---
description: 쿼리 매개 변수는 매니페스트 서버에 요청을 보낸 클라이언트 종류와 해당 클라이언트가 매니페스트 서버에서 수행할 작업을 알려줍니다. 일부 포맷은 필수이며 일부 포맷은 허용되는 특정 값을 갖습니다.
seo-description: 쿼리 매개 변수는 매니페스트 서버에 요청을 보낸 클라이언트 종류와 해당 클라이언트가 매니페스트 서버에서 수행할 작업을 알려줍니다. 일부 포맷은 필수이며 일부 포맷은 허용되는 특정 값을 갖습니다.
seo-title: 매니페스트 서버 쿼리 매개 변수
title: 매니페스트 서버 쿼리 매개 변수
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 매니페스트 서버 쿼리 매개 변수 {#manifest-server-query-parameters}

쿼리 매개 변수는 매니페스트 서버에 요청을 보낸 클라이언트 종류와 해당 클라이언트가 매니페스트 서버에서 수행할 작업을 알려줍니다. 일부 포맷은 필수이며 일부 포맷은 허용되는 특정 값을 갖습니다.

전체 URL 파섹 `parameterName=value` `Base URL?name1=value1&name2=value2& . . .&name n=value n`

## 인식된 매개 변수 {#section_072845B7FA94468C8068E9092983C9E6}

매니페스트 서버는 다음 매개 변수를 인식합니다. 인식할 수 없는 모든 매개 변수와 함께 광고 서버에 전달하거나 처리합니다.

| 키 | 설명 | 필수 | 유효한 값 |
|--- |--- |--- |--- |
| `__sid__` | 매니페스트 서버가 세션 ID를 생성하는 데 사용하는 고유 ID입니다. | 예 | 영숫자 |
| g | 클라이언트 장치 유형 | 타깃팅 규칙이 장치 유형에 따라 달라질 때 | 클라이언트 유형( [Zendesk](https://adobeprimetime.zendesk.com) 액세스 필요)의 목록을 참조하십시오. |
| k | 사용자 지정 광고 타깃팅을 위한 키워드 | 아니요 | key1=value1;key2=value2; 형식의 URL-safe 문자열... |
| u | Primetime 광고 삽입 자산 ID. | 예 | MD5 해시 값 |
| z | 자산에 대한 Primetime 광고 삽입 영역 ID. | 예 | 정수 |
| enableC3 | 클라이언트가 C3 창에 있습니다. true이면 로컬 가용 공간만 바꿉니다.그렇지 않으면 사용 가능한 모든 항목을 바꿉니다. | 아니요 | 부울 |
| live | 컨텐츠가 실시간 또는 VOD(Video On-Demand) 스트림인지 여부를 나타냅니다. | Akamai Ad Scaler 또는 iOS Safari 클라이언트 | 부울 |
| pabimode | [부분 광고 중단 삽입](../../msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) 지원 활성화 true이면 활성화 또는 false이면 비활성화 시작 | 아니요(기본값은 비활성화됨) | start, true 또는 false |
| padwindow | 광고 연결 창의 지속 시간(초):DVR 사용자가 스트림에 참여할 때 광고를 찾을 때까지의 거리입니다. | 아니오(기본값 = 1800) | 0 - 1800 |
| ptissetid | 게시자가 할당 및 유지 관리하는 컨텐츠의 고유 ID입니다. | Akamai Ad Scaler | URL-safe 문자열 |
| ptcdn | 트랜스코딩된 자산을 호스팅할 하나 이상의 CDN 목록입니다. 다중 [CDN 지원을 참조하십시오](../../creative-repackaging-service/multi-cdn-supportt.md). | 아니요(기본값=Akamai) | 예:Akamai, Level3, Limelight, Comcast |
| ptcueformat | M3U8에 있는 사용자 지정 광고 큐 형식의 이름입니다. | 아니요 | DPIimple, DPIcte35, Elements, NBC, NFL 또는 Turner |
| ptfailover | 마스터 재생 목록에 지정된 기본 및 장애 조치 스트림을 식별하고 분리형 세트로 처리하도록 매니페스트 서버에 신호를 보냅니다. 따라서 장애 조치를 용이하게 하고 시간 오류를 방지합니다. (Apple HLS 장치에만 해당) HLS [플레이어 전환](../../msapi-topics/ms-insert-ads/hls-switching-to-failover.md) 활성화를 참조하십시오. | 아니요 | true |
| ptmulticall | true로 설정된 경우 FER에 대한 여러 Auditude 광고 호출이 수행되었습니다.광고 중단마다 하나씩.  없거나 false로 설정된 경우 FER용 Auditude에 대해 하나의 광고 호출이 수행됩니다. | 아니요 | 부울 참고: 다음 요구 사항: <ul><li>ptcueformat 매개 변수는 nbc로 설정해야 합니다.</li><li>pttimeline 매개 변수는 무시됩니다.</li></ul> |
| ptplayer | 요청을 수행하는 플레이어입니다. | iOS/Safari | ios-mobileweb |
| 트렌드 | 광고 삽입으로 자동 생성되어 Akamai에서 사용됩니다. 추가하거나 제거하지 마십시오. | Akamai Ad Scaler |  |
| pttagds | EXT- [X- 불연속성- 시퀀스 태그](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) 활성화 | 아니요 | true - 매니페스트 서버는 전송한 각 m3u8 파일의 컨텐츠 앞에 시퀀스 태그를 포함합니다.매개 변수가 없거나 true가 아닌 경우 매니페스트 서버에 시퀀스 태그가 포함되지 않습니다. |
| pttimeline | 광고 배치 및 컨텐츠에 대해 원하는 타임라인을 포함하는 문자열입니다. 이 타임라인은 컨텐츠 스트림의 광고를 무시합니다. | 아니요 | VOD 타임라인( [VOD 타임라인 포맷](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)참조) |
| pttoken | TS 세그먼트 인증 토큰 활성화 참고: Akamai CDN 토큰만 지원됨 | TS 세그먼트 인증 토큰의 경우 | 부울 |
| pttrackingmode | 광고 추적 활성화;사용자 지정 클라이언트측(단순), 서버측(sstm) 또는 하이브리드(단순) 중 하나. | 아니요 | 단순, sstm 또는 간단한 참고 사항: 이 매개 변수가 포함되지 않으면 #EX-X-MARKER가 매니페스트에 삽입됩니다. EXT [-X-MARKER 지시문을 참조하십시오](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| pttrackingposition | 매니페스트 서버에 광고 추적 정보만 반환하도록 지시합니다. 부트스트랩 요청에서 이 매개 변수를 지정하지 마십시오. | 클라이언트측 추적 | 영숫자 참고: 매니페스트 서버는 전달된 모든 값을 무시합니다. 그러나 null 또는 빈 문자열을 전달하는 경우 매니페스트 서버는 추적 정보 대신 M3U8을 반환합니다. |
| pttrackingversion | 클라이언트측 추적 정보의 형식 버전입니다. | 클라이언트측 추적 | v1, v2, v3 또는 vmap |
| scteTracking | JSON V2 사이드카에서 SCTE 추적 정보를 가져오기 전에 M3U8을 반입합니다.  <br/>이 매개 변수는 M3U8을 가져오는 플레이어에서 검색해야 하는 SCTE 태그 정보를 매니페스트 서버에 나타냅니다. | 아니요(기본값: false ) | 참 또는 거짓 메모: SCTE-35 데이터는 다음과 같은 쿼리 매개 변수 값의 조합으로 JSON sidecar에서 반환됩니다. <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35` </li><li>pttrackingversion=v2 </li><li>scteTracking=true</li></ul> |
| vecargetmultiplier | 라이브 포인트의 세그먼트 수 프리롤 오프셋이 다음을 사용하여 구성됩니다.  `(  vetargetmultiplier  *  targetduration ) +  vebufferlength` 참고 <br/><br/>****: 라이브/선형 전용 | 아니요(기본값: 3.0 ) | 부동 |
| vebufferLength | 라이브 포인트 메모의 시간(초): 라이브/선형 전용 | 아니요(기본값: 3.0 ) | 부동 |
