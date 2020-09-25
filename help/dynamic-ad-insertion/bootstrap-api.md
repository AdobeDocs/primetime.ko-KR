---
title: Bootstrap API
description: null
translation-type: tm+mt
source-git-commit: aa43834fea161c537c448b7616c9bd8f779d1a74
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# Bootstrap API {#bootstrap-api}

필수 매개 변수부트스트랩 생성

## 매개 변수 설명 {#parameter-description}

| parameter | description | formats |
|---|---|---|
| pabimode | 라이브 스트림에 대해 [부분 광고 중단 삽입](ad-insertion-live-linear-stream.md#partial-ad-break-support) 기능을 활성화합니다. 사용 안 함(기본값 사용 안 함)을 사용하도록 설정하려면 true | HLS/대시 |
| padwindow | 룩백 광고 결정 창의 기간(초) — DVR 사용자가 스트림에 참여할 때 Primetime Ad Insertion이 광고 신호를 찾는 시간 값이 0이면 초기 매니페스트에서 mid-roll 광고 결정이 비활성화되며, 첫 번째 업데이트 후에만 의사 결정이 다시 시작됩니다. 이 매개 변수는 단 몇 초만 지속될 수 있는 세션(채널 전환)에 광고 삽입을 비활성화하는 데 유용합니다. 가능한 값:숫자 문자열 0-1800(기본값 1800) | HLS만 |
| ptissetid | 게시자가 할당하고 유지 관리하는 컨텐츠의 고유 ID.  Akamai Ad Scaler와 함께 사용할 때 필요합니다. | HLS/대시 |
| ptcdn | 트랜스코딩된 자산을 호스팅할 하나 이상의 CDN 목록. 자세한 내용은 다중 CDN [지원을 참조하십시오](multi-cdn-support.md). 가능한 값:akamai, level3, llnw(limelight network), comcast기본적으로 Primetime Ad Insertion CDN이 사용됩니다 | HLS/대시 |
| ptcueformat | 광고 결정을 수행할 지정된 태그 형식(예: scte35). 가능한 값:dpisimple, dpiscte35, elements For custom cue formats, please contact your technical account representative for your use case | HLS/대시 |
| ptfailover | 매니페스트 서버에서 마스터 재생 목록에 지정된 기본 및 장애 조치 스트림을 식별하고 분리형 세트로 처리하도록 신호를 보냅니다. 따라서 장애 조치를 용이하게 하고 시간 오류를 방지합니다. (Apple HLS 장치에만 해당) 자세한 내용은 HLS [플레이어 전환 활성화를 참조하십시오.](hls-switching-to-failover.md) | HLS만 |
| ptmulticall | 활성화된 경우 VOD 자산에 있는 각 기능에 대해 별도의 광고 요청이 수행됩니다.  기본적으로 Primetime Ad Insertion은 모든 사용 가능한 정보를 수집하여 한 번의 요청으로 광고 서버로 전송합니다. 사용 안 함(기본값 사용 안 함)을 사용하도록 설정하려면 true | HLS/대시 |
| pttagds | HLS 헤더에 EXT-X-DISCONTINUITY-SEQUENCE 태그를 삽입하도록 활성화합니다.가능한 값:true를 사용하여 비활성화하도록 설정(기본 비활성화됨) | HLS만 |
| pttimeline | 광고 배치 및 컨텐츠에 대해 원하는 타임라인을 포함하는 문자열. 이 타임라인은 컨텐츠 스트림에서 광고를 대체합니다. [ VOD 타임라인 포맷 보기 ] | HLS/대시 |
| pttoken | CDN의 가능한 값에 대한 컨텐츠 조각/세그먼트 인증 토큰 보호 체계를 활성화합니다.akamai, llnw (limelight), ctl(centurylink)(기본 토큰화 사용 안 함) | HLS/대시 |
| pttrackingmode | 광고 추적 구성표 활성화:가능한 값:하이브리드 클라이언트/서버 광고 추적에 대한 서버측 광고 추적을 위한 단순 클라이언트측 광고 추적스스트림(기본적으로 광고 추적이 수행되지 않음) | HLS/대시 |
| pttrackingversion |  |  |
| ptadtimeout(예: 20.9.2) |  |  |
| ptparallstream (as in 20.9.3) |  |  |
