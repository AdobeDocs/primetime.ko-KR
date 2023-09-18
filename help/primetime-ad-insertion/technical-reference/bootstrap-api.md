---
title: BOOTSTRAP API
description: BOOTSTRAP API
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# BOOTSTRAP API {#bootstrap-api}

Bootstrap API는 일반적으로 클라이언트/비디오 재생 API로 전송되는 URL입니다.  구성할 수 있는 옵션 및 매개 변수에 대해서는 다음을 참조하십시오. [Bootstrap API 매개 변수](#bootstrap-api-parameters).

## 매니페스트 서버에 명령 보내기 {#send-a-command-to-the-manifest-server}

1. 보내기 `HTTP GET` 다음 패턴을 사용하여 생성된 부트스트랩 URL에 대한 요청:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **파일 확장명** 정의됨. `.m3u8` 대상 매니페스트가 HLS인 경우 `.mpd` 대상 매니페스트가 DASH에 있는 경우

   * **게시자 자산 ID** 필수. 특정 콘텐츠에 대한 게시자의 고유 ID입니다.

   * **컨텐츠 URL** 필수. 매니페스트 서버 URL 내에서 안전하도록 인코딩된 Base64인 콘텐츠 M3U8 파일의 URL입니다. 비트 전송률 스트림이 하나만 있는 경우에도 콘텐츠 URL은 변형 M3U8 파일을 가리켜야 합니다.

   * **쿼리 매개 변수** 이는 요청의 가장 다양한 부분을 구성합니다. 매니페스트 서버에는 어떤 종류의 클라이언트가 요청을 하고 있는지, 매니페스트 서버가 무엇을 하기를 원하는지 알려줍니다.

   예:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP 요청과 HTTPS 요청 비교**

   매니페스트 서버는 클라이언트 요청의 동일한 HTTP 프로토콜을 사용하여 URL을 만듭니다. 플레이어가 비보안 HTTP(http) 요청을 수행하면 매니페스트 서버는 http 프로토콜이 있는 매니페스트 URL 및 Auditude 추적 URL을 반환합니다. 플레이어가 보안 HTTP(https) 연결, 매니페스트 서버를 만들면 https 프로토콜이 있는 매니페스트 URL 및 Auditude 추적 URL이 반환됩니다.

   >[!NOTE]
   >
   >매니페스트 서버는 타사 추적 비콘의 프로토콜(HTTP 또는 HTTPS)을 변경할 수 없습니다. 원하는 프로토콜을 구성하려면 콘텐츠 및 서드파티 광고 공급자에게 문의해야 합니다.  세그먼트 URL 프로토콜은 변경할 수 있지만 기본적으로 대상 매니페스트에 정의된 것과 동일한 프로토콜을 사용합니다.

## Bootstrap API 매개 변수 {#bootstrap-api-parameters}

쿼리 매개 변수는 매니페스트 서버에서 요청을 보낸 클라이언트 종류와 매니페스트 서버에서 수행하려는 작업을 알려 줍니다. 일부는 필수이며 일부는 특정 허용 형식 또는 값을 갖습니다.
전체 URL은 기본 URL 뒤에 물음표가 붙은 다음, `parameterName=value` 인수는 앰퍼샌드로 구분됩니다. 예를 들어, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

매니페스트 서버는 다음 매개 변수를 인식합니다. 모든 쿼리 문자열\
매개 변수가 광고 서버에 전달됩니다.

| 매개 변수 | 설명 | 형식 |
|---|---|---|
| _sid_ | 매니페스트 서버가 세션 ID를 생성하는 데 사용할 고유 ID입니다. | DASH/HLS 모두에 필요 |
| live | 전달된 콘텐츠 항목이 라이브 스트림임을 Primetime Ad Insertion에게 알립니다.  이 매개 변수가 전달되지 않으면 Primetime Ad 삽입에서는 매니페스트가 live인지 vod인지를 확인하기 위해 초기 매니페스트 호출에 대한 보조 요청을 하게 됩니다.<br>가능한 값:<br>라이브 컨텐츠에 true<br>vod 컨텐츠에 대해 false<br>자동 감지용 생략 | HLS의 경우 선택 사항입니다.  대시에 필요 |
| z | Primetime Ad Insertion에 제공해야 하는 에셋의 영역 ID입니다. Adobe 기술 계정 관리자가 제공합니다. | DASH/HLS 모두에 필요 |
| 파비모드 | 사용 [부분 광고 브레이크 삽입](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) 라이브 스트림용<br>가능한 값:<br>활성화하려면 true<br>비활성화하려면 생략(기본값 비활성화) | HLS/대시 |
| ptadtimeout | 다운스트림 공급자가 응답하는 데 너무 오래 걸리는 경우 전체 광고 해결 시간을 제한할 수 있습니다.  오래 실행되는 응답으로 인해 재생에 문제가 발생할 수 있으므로 Primetime DAI는 특정 시간 제한 내에 응답을 강제 적용할 수 있습니다.<br>가능한 값:<br>숫자 문자열(밀리초)<br>비활성화하려면 생략(기본값 비활성화) | HLS/대시 |
| ptadwindow | 전환 확인 Ad Insertion 결정 창의 기간(초) - DVR 사용자가 스트림에 참여할 때 Primetime 사용자가 광고 큐를 찾는 데 얼마나 오래 걸릴지 여부입니다. 값이 0이면 초기 매니페스트에서 미드롤 광고 의사 결정이 비활성화되고, 첫 번째 업데이트 후에만 의사 결정이 다시 시작됩니다. 이 매개 변수는 몇 초만 지속될 수 있는(예: 채널 뒤집기) 세션에 대한 광고 삽입을 비활성화하는 데 유용합니다.<br>가능한 값:<br>숫자 문자열 0-1800(기본값 1800) | HLS만 |
| ptassetid | 게시자가 할당 및 유지 관리하는 콘텐츠에 대한 고유 ID.  Akamai Ad Scaler와 함께 사용할 때 필요합니다. | HLS/대시 |
| ptcdn | 트랜스코딩된 에셋을 호스팅할 하나 이상의 CDN 목록입니다. 자세한 내용은 [게재 및 보관](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>가능한 값:<br>akamai, level3, llnw(각광 네트워크), comcast.<br>기본적으로 Primetime Ad Insertion CDN이 사용됩니다. | HLS/대시 |
| ptcueformat | 광고 결정을 수행할 지정된 태그 형식(예: scte35).<br>가능한 값:<br>dpissimple, dpiscte35, 원소<br>사용자 지정 큐 형식은 기술 계정 담당자에게 문의하여 사용 사례에 사용할 값을 얻으십시오 | HLS/대시 |
| ptfailover | 매니페스트 서버에 신호를 보내 마스터 재생 목록에 지정된 주 스트림과 장애 조치(failover) 스트림을 식별하고 분리된 집합으로 처리합니다. 이를 통해 페일오버를 원활하게 수행하고 타이밍 오류를 방지할 수 있습니다. (Apple HLS 장치만 해당) 자세한 내용은 [HLS 플레이어 전환 촉진](hls-switching-to-failover.md) | HLS만 |
| ptmulticall | 활성화되면 VOD 자산에 있는 각 가용성에 대해 별도의 광고 요청이 만들어집니다.  기본적으로 Primetime Ad Insertion은 사용 가능한 모든 정보를 수집하여 한 번의 요청으로 광고 서버로 전송합니다. 가능한 값:활성화하려면 true, <br>비활성화하려면 생략(기본값 비활성화) | HLS/대시 |
| ptparallelstream | CMAF 중복 제거된 오디오 또는 비디오 스트림을 동시에 요청하는 플레이어를 사용하는 고객이 오디오 및 비디오 트랙의 광고가 일관되도록 합니다. | HLS만 |
| ptprotoswitch | 기술 지원 담당자가 일반적으로 설정하는 명명된 매니페스트 재작성 규칙 및 광고 가져오기 규칙을 사용하도록 설정합니다.<br>예: adfetch_fw, cdn_akm | HLS/대시 |
| 패키지 | EXT-X-DISCONTINUITY-SEQUENCE 태그를 HLS 헤더에 삽입할 수 있습니다. 가능한 값:true를 활성화하려면 생략(기본값 비활성화) | HLS만 |
| pttimeline | 컨텐츠 스트림의 광고 브레이크를 오버라이드하는 광고 배치 및 컨텐츠에 대해 원하는 타임라인을 포함하는 문자열입니다. [VOD 타임라인 형식 을 참조하십시오.] | HLS/대시 |
| pttoken | CDN에 대해 컨텐츠 조각/세그먼트 인증 토큰 보호 체계 활성화<br>가능한 값:<br>akamai, lnw(limelight), ctl(centurylink)(기본 토큰화가 비활성화됨) | HLS/대시 |
| pttrackingmode | 광고 추적 스키마를 활성화합니다.<br>가능한 값:<br>클라이언트측 광고 추적을 위한 간단한 방법<br>서버측 광고 추적을 위한 sstm<br>하이브리드 클라이언트/서버 광고 추적을 위한 simplestm(기본적으로 광고 추적이 수행되지 않음) | HLS/대시 |
| pttrackingposition | 매니페스트 서버에서 광고 추적 정보만 반환하도록 지시합니다. 부트스트랩 요청에서 이 매개 변수를 지정하지 마십시오.<br>참고: 매니페스트 서버는 전달된 모든 값을 무시합니다. 그러나 null 또는 빈 문자열을 전달하면 매니페스트 서버는 M3U8을 반환합니다 | HLS/대시<br>클라이언트측 추적 |
| pttrackingversion | 반환할 형식 버전을 설정합니다.<br>가능한 값:<br>v1, v2, v3 또는 vmap | HLS/대시<br>클라이언트측 추적 |
| scteTracking | 이 매개 변수는 M3U8을 가져오는 플레이어에 SCTE 태그 정보를 검색해야 함을 매니페스트 서버에 나타냅니다.<br>가능한 값:<br>true 또는 false(기본값 false)<br>참고: SCTE-35 데이터는 다음과 같은 쿼리 매개 변수 값의 조합과 함께 JSON 사이드카에 반환됩니다.<br>ptcueformat=turner | 원소 | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | HLS만 |
| vetargetmultiplier | 라이브 포인트의 세그먼트 수 프리롤 오프셋은 ( vetargetmultiplier * targetduration ) + vebufferlength를 사용하여 구성됩니다.<br>참고: 이 매개 변수는 라이브/선형 HLS 스트림에만 적용됩니다<br>가능한 값:<br>숫자 부동 소수점<br>(기본값: 3.0 - HLS 사양과 동일) | HLS만 |
| vebufferLength | 라이브 포인트에서 vetargetmultiplier와 함께 사용되는 초 수입니다.<br>참고: 이 매개 변수는 라이브/선형 HLS 스트림에만 적용됩니다<br>가능한 값:<br>숫자 부동 소수점<br>(기본값: 3.0) | HLS만 |
