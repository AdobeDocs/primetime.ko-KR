---
title: 광고 추적 설정
description: 광고 추적 설정
exl-id: b5ebad0f-4e20-456a-892d-4c981ab26e51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 광고 추적 설정 {#ser-up-ad-tracking}

대부분의 광고주는 광고를 시청한 시간, 기간 및 성공 방법에 대한 정보를 필요로 합니다. Primetime Ad Insertion은 클라이언트측, 서버측 및 하이브리드 광고 추적을 지원하여 이 정보를 유연하게 수집할 수 있습니다.

## VMAP/JSON을 사용한 클라이언트측 광고 추적 {#client-side-ad-tracking-vmap-json}

클라이언트측 광고 추적에서 서버는 광고에 결합된 재생 목록과 함께 추적 이벤트 및 URL을 지정하는 JSON, VMAP 또는 매니페스트 내 구조를 클라이언트에 보냅니다.

클라이언트측 광고 추적을 활성화하려면 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>설정 `pttrackingmode=simple` 는 초기 부트스트랩 API 요청이 HLS 또는 DASH 문서가 아닌 JSON 응답을 반환하게 합니다.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## 서버측 광고 추적 {#server-side-ad-tracking}

이 방법을 사용하면 광고 추적 데이터가 전적으로 서버측에서 계산됩니다. 이 기능은 클라이언트 응용 프로그램을 업데이트할 수 없는 경우에 유용합니다. 그러나 서버측 광고 추적은 클라이언트측 재생 활동과 일치하지 않을 수 있습니다. 예를 들어 서버는 최종 사용자가 전체 광고를 보지 않더라도 세그먼트가 전달된 후 광고가 재생되는 것으로 간주합니다.

서버측 광고 추적을 활성화하려면 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

다음을 참조하십시오 `pttrackingmode` 섹션 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

모든 광고 추적 비콘은 다음 HTTP 요청 헤더와 함께 전송됩니다.

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

이러한 값에는 클라이언트/플레이어 사용자 에이전트와 클라이언트 IP 주소가 포함됩니다.

## 하이브리드 광고 추적 {#hybrid-ad-tracking}

이 접근 방식은 서버측 추적과 유사하지만, 클라이언트 애플리케이션은 자세한 추적 정보를 위해 Primetime Ad Insertion의 사이드카도 요청합니다. 하이브리드 광고 추적은 개별 광고 추적 URL을 전송하기 위해 Primetime Ad Insertion을 계속 사용하는 동안 오버레이 및 동반자와 같은 비선형 광고를 클라이언트 애플리케이션에 전달할 수 있습니다.
하이브리드 광고 추적을 활성화하려면 다음을 참조하십시오 `pttrackingmode` 의 매개 변수 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
