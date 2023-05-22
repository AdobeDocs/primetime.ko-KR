---
title: 매니페스트 서버 쿼리 매개 변수
description: 쿼리 매개 변수는 매니페스트 서버에서 요청을 보낸 클라이언트 종류와 매니페스트 서버에서 수행하려는 작업을 알려 줍니다. 일부는 필수이며 일부는 특정 허용 형식 또는 값을 갖습니다.
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# 매니페스트 서버 쿼리 매개 변수 {#ms-query-params}

쿼리 매개 변수는 매니페스트 서버에서 요청을 보낸 클라이언트 종류와 매니페스트 서버에서 수행하려는 작업을 알려 줍니다. 일부는 필수이며 일부는 특정 허용 형식 또는 값을 갖습니다.

전체 URL은 기본 URL 뒤에 물음표가 붙은 다음, `parameterName=value` 앰퍼샌드로 구분된 인수 `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## 인식된 매개 변수 {#section_072845B7FA94468C8068E9092983C9E6}

매니페스트 서버는 다음 매개 변수를 인식합니다. 이를 처리하거나 인식되지 않은 모든 매개 변수와 함께 광고 서버에 전달합니다.

| 키 | 설명 | 필수 | 유효한 값 |
|---|---|---|---|
| `__sid__` | 매니페스트 서버가 세션 ID를 생성하는 데 사용하는 고유 ID입니다. | 예 | 영숫자 |
| g | 클라이언트 장치 유형 | 장치 유형에 따라 타겟팅 규칙이 달라지는 경우 | 다음 위치에서 목록 보기: [클라이언트 유형](https://adobeprimetime.zendesk.com). Zendesk 액세스 권한이 필요합니다. |
| k | 사용자 지정 광고 타깃팅용 키워드 | 아니요 | 형식의 URL 안전 문자열 `key1=value1;key2=value2;. . .` |
| u | Primetime 광고 삽입 자산 ID. | 예 | MD5 해시 값 |
| z | 자산에 대한 Primetime 광고 삽입 영역 ID. | 예 | 정수 |
| enableC3 | 클라이언트가 C3 창에 있습니다. true이면 로컬 사용 가능 항목만 바꾸고, 그렇지 않으면 모든 사용 가능 항목을 바꿉니다. | 아니요 | 부울 |
| live | 콘텐츠가 라이브 스트림인지 VOD 스트림인지 여부를 나타냅니다. | Akamai Ad Scaler 또는 iOS Safari 클라이언트 | 부울 |
| `pabimode` | [부분 광고 브레이크 삽입 활성화](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) 지원. <br> true이거나 시작하는 경우 활성화합니다.<br> false인 경우 비활성화합니다. | 아니요 (기본값은 비활성화됨) | start, true 또는 false |
| `ptadwindow` | 광고 결합 기간(초): DVR 사용자가 스트림에 참여할 때 광고를 찾는 데 얼마나 오래 걸렸습니까? | 아니요(기본값 = 1800) | 0~1800 |
| `ptassetid` | 게시자가 할당 및 유지 관리하는 콘텐츠에 대한 고유 ID. | Akamai 광고 스케일러 | URL 안전 문자열 |
| `ptcdn` | 트랜스코딩된 에셋을 호스팅할 하나 이상의 CDN 목록입니다. 다음을 참조하십시오 [다중 CDN 지원](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | 아니요(기본값=Akamai) | 예: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | M3U8에 있는 사용자 지정 광고 큐 형식의 이름입니다. | 아니요 | DPISimple, DPIScte35, Elemental, NBC, NFL 또는 Turner |
| `ptfailover` | 매니페스트 서버에 신호를 보내 마스터 재생 목록에 지정된 주 스트림과 장애 조치(failover) 스트림을 식별하고 분리된 집합으로 처리합니다. 이를 통해 페일오버를 원활하게 수행하고 타이밍 오류를 방지할 수 있습니다. (Apple HLS 장치만 해당). 다음을 참조하십시오  [HLS 플레이어 전환 촉진](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | 아니요 | true |
| `ptmulticall` | True로 설정하면 FER에 대한 여러 Auditude 광고 호출이 수행되며, 각 광고 브레이크에 대해 한 번씩 수행됩니다. 없거나 false로 설정된 경우 FER에 대한 하나의 광고 호출이 감사됩니다. | 아니요 | 부울 <br> **참고**: 다음 요구 사항: <ul><li>`ptcueformat` 매개 변수는 nbc로 설정해야 합니다.</li><li>pttimeline 매개 변수는 무시됩니다.</li></ul> |
| `ptplayer` | 요청을 하는 플레이어. | iOS/Safari | ios-mobileweb |
| `ptrendition` | 광고 삽입으로 자동 생성되고 Akamai에서 사용됩니다. 추가하거나 제거하지 마십시오. | Akamai 광고 스케일러 |  |
| `pttagds` | 사용 [EXT-X- 불연속- 시퀀스](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) 태그 | 아니요 | true - 매니페스트 서버는 각 m3u8 파일에서 콘텐츠를 전송하기 전에 시퀀스 태그를 포함합니다. 매개 변수가 없거나 true가 아니면 매니페스트 서버는 시퀀스 태그를 포함하지 않습니다. |
| `pttimeline` | 컨텐츠 스트림의 광고 브레이크를 오버라이드하는 광고 배치 및 컨텐츠에 대해 원하는 타임라인을 포함하는 문자열입니다. | 아니요 | [VOD 타임라인](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | TS 세그먼트 인증 토큰을 활성화합니다.<br> **참고**: Akamai CDN 토큰만 지원됨 | TS 세그먼트 인증 토큰의 경우 | 부울 |
| `pttrackingmode` | 사용자 지정 클라이언트측(단순), 서버측(sstm) 또는 하이브리드(simplesstm)의 광고 추적을 활성화합니다. | 아니요 | simple, sstm 또는 simplesstm.<br> **참고**: 이 매개 변수가 포함되지 않으면 #EX-X-MARKER이 매니페스트에 삽입됩니다. 다음을 참조하십시오 [EXT-X-MARKER 지시문](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | 매니페스트 서버에서 광고 추적 정보만 반환하도록 지시합니다. 부트스트랩 요청에서 이 매개 변수를 지정하지 마십시오. | 클라이언트측 추적 | 영숫자 참고: 매니페스트 서버는 전달된 모든 값을 무시합니다. 그러나 null 또는 빈 문자열을 전달하면 매니페스트 서버는 추적 정보 대신 M3U8을 반환합니다. |
| `pttrackingversion` | 클라이언트측 추적 정보의 형식 버전. | 클라이언트측 추적 | v1, v2, v3 또는 vmap |
| `scteTracking` | JSON V2 사이드카에서 SCTE 추적 정보를 가져오기 전에 M3U8 을 가져옵니다. <br>이 매개 변수는 M3U8을 가져오는 플레이어에 SCTE 태그 정보를 검색해야 함을 매니페스트 서버에 나타냅니다. | 아니요(기본값: false) | true 또는 false. <br> **참고**: SCTE-35 데이터가 다음과 같은 쿼리 매개 변수 값의 조합과 함께 JSON 사이드카에서 반환됩니다. <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | 라이브 포인트의 세그먼트 수 프리롤 오프셋은 다음을 사용하여 구성됩니다. `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**참고**: 라이브/선형만 | 아니요(기본값: 3.0) | 부동 |
| `vebufferLength` | 라이브 포인트에서 보낸 시간(초)입니다. **참고**: 라이브/선형만 해당. | 아니요(기본값: 3.0) | 부동 |
