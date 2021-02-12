---
title: Bootstrap API
description: 'Bootstrap API '
translation-type: tm+mt
source-git-commit: bf99c76bbbb67560adc675cf84297b8d3b04e19d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# Bootstrap API {#bootstrap-api}

Bootstrap API는 일반적으로 클라이언트/비디오 재생 API로 전송되는 URL입니다.  구성할 수 있는 옵션 및 매개 변수에 대해서는 [Bootstrap API 매개 변수](#bootstrap-api-parameters)를 참조하십시오.

## 매니페스트 서버 {#send-a-command-to-the-manifest-server}에 명령 보내기

1. 다음 패턴을 사용하여 구성한 부트스트랩 URL에 대해 `HTTP GET` 요청을 보냅니다.

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **파일 확장자** 가 정의되었습니다. `.m3u8` 대상 매니페스트가 HLS인 경우 대상 매니페스트가 DASH에  `.mpd` 있는 경우

   * **PublisherAssetIDRidered** 가 필요합니다. 특정 컨텐츠에 대한 게시자의 고유 ID.

   * **컨텐츠** URLRequired. 매니페스트 서버 URL 내에서 안전하도록 인코딩된 M3U8 파일의 URL입니다. 콘텐츠 URL은 비트 전송률 스트림이 하나만 있는 경우에도 변형 M3U8 파일을 가리켜야 합니다.

   * **쿼리** 매개 변수이 매개 변수는 요청의 가장 다양한 부분을 구성합니다. 매니페스트 서버에는 요청을 수행하는 클라이언트 종류와 매니페스트 서버가 수행할 작업을 알려 줍니다.

   예:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP와 HTTPS 요청 비교**

   매니페스트 서버는 클라이언트의 요청과 동일한 HTTP 프로토콜을 사용하여 URL을 만듭니다. 플레이어가 비보안 HTTP(http) 요청을 수행하는 경우 매니페스트 서버는 http 프로토콜을 사용하여 매니페스트 URL 및 Auditude 추적 URL을 반환합니다. 플레이어가 보안 HTTP(https) 연결, 매니페스트 서버를 만들면 매니페스트 URL 및 Auditude 추적 URL을 https 프로토콜로 반환합니다.

   >[!NOTE]
   >
   >매니페스트 서버는 타사 추적 비콘의 프로토콜(HTTP 또는 HTTPS)을 변경할 수 없습니다. 원하는 프로토콜을 구성하려면 컨텐츠와 타사 광고 공급자에 문의해야 합니다.  세그먼트 URL 프로토콜은 변경할 수 있지만 기본적으로 대상 매니페스트에 정의된 것과 동일한 프로토콜을 사용합니다.

## Bootstrap API 매개 변수 {#bootstrap-api-parameters}

쿼리 매개 변수는 매니페스트 서버에 요청을 보낸 클라이언트 종류와 매니페스트 서버가 수행할 작업을 알려 줍니다. 일부 형식은 필수이며 일부는 허용되는 특정 형식 또는 값을 가집니다.
전체 URL은 기본 URL 뒤에 물음표가 표시된 다음 `parameterName=value` 인수가 앰퍼맨드로 구분됩니다. 예: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

매니페스트 서버는 다음 매개 변수를 인식합니다. 모든 쿼리 문자열\
매개 변수가 광고 서버에 전달됩니다.

| parameter | description | formats |
|---|---|---|
| _sid_ | 매니페스트 서버가 세션 ID를 생성하는 데 사용할 고유 ID입니다. | 대시/HLS 모두에 필요 |
| live | 전달된 콘텐츠 항목이 라이브 스트림임을 Primetime Ad Insertion에 알립니다.  이 매개 변수가 전달되지 않은 경우 Primetime 광고 삽입은 매니페스트가 실시간 또는 vod인지 확인하기 위해 초기 매니페스트 호출에 보조 요청을 수행합니다.<br>가능한 값:실시간 컨텐츠의 경우 <br>true <br>, 자동 감지를 위한 <br>경우 false입니다. | HLS에 대한 선택 사항입니다.  DASH에 필요 |
| z | Primetime Ad Insertion에 제공해야 하는 에셋의 영역 ID입니다. Adobe 기술 계정 관리자가 제공합니다. | 대시/HLS 모두에 필요 |
| pabimode | 라이브 스트림에 대해 [부분 광고 나누기 삽입](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support)을 활성화합니다.<br>사용할 수 있는 값:<br>true로 설정하면 <br>생략(기본값 사용 안 함) | HLS/대시 |
| padtimeout | 다운스트림 제공자가 응답하는 데 시간이 너무 오래 걸리는 경우 전체 광고 해상도 시간을 제한할 수 있습니다.  실행 응답이 길면 재생과 관련된 문제가 발생할 수 있으므로 Primetime DAI는 특정 시간 제한 내에 응답을 제공할 수 있습니다.<br>가능한 값:<br>숫자 문자열(밀리초)입니다.<br>disable을 생략합니다(기본적으로 비활성화됨). | HLS/대시 |
| tadwindow | 룩백 광고 결정 창의 기간(초) — DVR 사용자가 스트림에 참여할 때 Primetime Ad Insertion이 광고 큐를 찾는 시간을 말합니다. 값이 0이면 초기 매니페스트에서 mid-roll 광고 의사 결정이 비활성화되며, 첫 번째 업데이트 후에만 의사 결정이 다시 시작됩니다. 이 매개 변수는 몇 초만 지속될 수 있는(채널 뒤집을 수도 있음) 세션에 광고 삽입을 비활성화하는 데 유용합니다.<br>가능한 값: <br>숫자 문자열 0-1800(기본값 1800) | HLS만 |
| ptissetid | 게시자가 할당하고 유지 관리하는 컨텐츠의 고유 ID.  Akamai Ad Scaler와 함께 사용할 때 필요합니다. | HLS/대시 |
| ptcdn | 코드 변환된 에셋을 호스팅할 하나 이상의 CDN 목록. 자세한 내용은 [배달 및 저장 공간](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md)을 참조하십시오.<br>가능한 값: <br>akamai, level3, llnw(limelight network), comcast.<br>기본적으로 Primetime Ad Insertion CDN이 사용됩니다. | HLS/대시 |
| ptcueformat | 광고 결정을 수행할 지정된 태그 형식(예: scte35).<br>가능한 값:<br>dpisimple, dpiscte35, elements사용자 지정 큐 <br>형식의 경우 기술 계정 담당자에게 문의하여 사용 사례에 사용할 값을 확인하십시오. | HLS/대시 |
| ptfailover | 매니페스트 서버에서 마스터 재생 목록에 지정된 기본 및 장애 조치 스트림을 식별하고 이를 분리형 세트로 처리하도록 합니다. 이를 통해 장애 조치를 용이하게 하고 시간 오류를 방지합니다. (Apple HLS 장치에만 해당) 자세한 내용은 [HLS 플레이어 전환 촉진](hls-switching-to-failover.md)을 참조하십시오. | HLS만 |
| ptmulticall | 활성화된 경우 VOD 자산에 있는 각 기능에 대해 별도의 광고 요청이 수행됩니다.  기본적으로 Primetime Ad Insertion은 이용 가능한 모든 정보를 수집하여 한 번의 요청으로 광고 서버로 전송합니다. 가능한 값:true to enable, <br>생략(기본값 사용 안 함) | HLS/대시 |
| pparallstream | 오디오 및 비디오 트랙의 광고가 일관되게 나타나도록 CMAF 요청 오디오 또는 비디오 스트림을 병렬로 요청하는 플레이어를 사용할 수 있습니다. | HLS만 |
| ptprotoswitch | 지정된 매니페스트 다시 쓰기 규칙 및 광고 가져오기 규칙을 활성화합니다. 이 규칙은 일반적으로 기술 지원 담당자가 설정합니다.<br>예:adfetch_fw, cdn_akm | HLS/대시 |
| pttagds | HLS 헤더에 EXT-X-DISCONTINUITY-SEQUENCE 태그를 삽입할 수 있도록 합니다.사용할 수 있는 값:true를 사용하여 disabled를 사용하도록 설정(기본적으로 비활성화됨) | HLS만 |
| pttimeline | 광고 배치 및 컨텐츠에 대해 원하는 타임라인을 포함하는 문자열을 반환합니다. 이 타임라인은 컨텐츠 스트림에서 광고를 무시합니다. [ VOD 타임라인 포맷 참조  ] | HLS/대시 |
| pttoken | CDN<br>가능한 값:<br>akamai, llnw(limelight), ctl(centurylink)(기본 토큰화는 비활성화됨)에 대한 컨텐츠 조각/세그먼트 인증 토큰 보호 체계를 활성화합니다. | HLS/대시 |
| pttrackingmode | 광고 추적 체계를 활성화합니다.<br>가능한 값:<br>간단한 클라이언트측 광고 <br>추적<br>ssm for server-side ad trackingsstm for hybrid client/server 광고 추적(기본적으로 광고 추적이 수행되지 않음) | HLS/대시 |
| pttrackingposition | 매니페스트 서버에 광고 추적 정보만 반환하도록 지시합니다. 부트스트랩 요청에서 이 매개 변수를 지정하지 마십시오.<br>참고:매니페스트 서버는 전달된 모든 값을 무시합니다. 그러나 null 또는 빈 문자열을 전달하는 경우 매니페스트 서버는 M3U8을 반환합니다 | HLS/DASH<br>클라이언트측 추적 |
| pttrackingversion | 반환할 형식 버전을 설정합니다.<br>가능한 값: <br>v1, v2, v3 또는 vmap | HLS/DASH<br>클라이언트측 추적 |
| scteTracking | 이 매개 변수는 M3U8을 가져오는 플레이어에서 SCTE 태그 정보를 검색해야 함을 매니페스트 서버에 나타냅니다.<br>가능한 값:<br>true 또는 false(기본값 false)<br>참고:SCTE-35 데이터는 쿼리 매개 변수 값의 다음 조합과 함께 JSON sidecar에 <br>반환됩니다.ptcueformat=turner | 원소 | nfl | DKPIcte35<br>pttrackingversion=v2<br>scteTracking=true<br> | HLS만 |
| vetargetmultiplier | 라이브 포인트의 세그먼트 수 프리롤 오프셋은 다음을 사용하여 구성됩니다.( vetargetmultiplier * targetduration ) + vebufferlength<br>참고:이 매개 변수는 라이브/선형 HLS 스트림에만 적용되며<br>가능한 값:<br>숫자 부동<br>(기본값:3.0 - HLS 사양과 동일) | HLS만 |
| vebufferLength | vetargetmultiplier와 함께 사용되는 라이브 포인트의 초 수입니다.<br>참고:이 매개 변수는 라이브/선형 HLS 스트림에만 적용가능한 <br>값:<br>숫자 부동<br>(기본값:3.0) | HLS만 |
