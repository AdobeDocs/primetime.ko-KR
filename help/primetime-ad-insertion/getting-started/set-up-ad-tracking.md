---
title: 광고 추적 설정
description: 광고 추적 설정
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# 광고 추적 설정 {#ser-up-ad-tracking}

대부분의 광고주는 광고가 언제, 얼마나 오래, 그리고 얼마나 성공적으로 보는지에 대한 정보를 필요로 합니다. Primetime Ad Insertion은 클라이언트측, 서버측 및 하이브리드 광고 추적을 지원하므로 이러한 정보를 유연하게 수집할 수 있습니다.

## VMAP/JSON {#client-side-ad-tracking-vmap-json}이(가) 있는 클라이언트측 광고 추적

클라이언트측 광고 추적에서 서버는 광고 스티칭된 재생 목록과 함께 추적 이벤트 및 URL을 지정하는 JSON, VMAP 또는 매니페스트 내 구조를 클라이언트에 전송합니다.

클라이언트측 광고 추적을 활성화하려면 [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)에서 다음 매개 변수를 지정합니다.

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>`pttrackingmode=simple`을 설정하면 초기 부트스트랩 API 요청이 HLS 또는 DASH 문서가 아닌 JSON 응답을 반환합니다.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## 서버측 광고 추적 {#server-side-ad-tracking}

이 방법을 사용하면 광고 추적 데이터가 서버측에서 모두 계산됩니다. 이 기능은 클라이언트 응용 프로그램을 업데이트할 수 없는 경우에 유용합니다. 그러나 서버측 광고 추적은 클라이언트측 재생 활동과 일치하지 않을 수 있습니다. 예를 들어, 최종 사용자가 전체 광고를 보지 않더라도 세그먼트가 전달된 후에 광고가 재생되도록 간주합니다.

서버측 광고 추적을 활성화하려면 [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)에서 다음 매개 변수를 지정합니다.

`pttrackingmode=sstm`

[Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)의 `pttrackingmode` 섹션을 참조하십시오.

모든 광고 추적 비콘은 다음 HTTP 요청 헤더로 전송됩니다.

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

이 값에는 클라이언트/플레이어 사용자 에이전트 및 클라이언트 IP 주소가 포함되어 있습니다.

## 하이브리드 광고 추적 {#hybrid-ad-tracking}

이 방법은 서버측 추적과 비슷하지만 클라이언트 애플리케이션이 Primetime Ad Insertion의 사이드카어에게 자세한 추적 정보를 요청합니다. 하이브리드 광고 추적은 오버레이 및 그와 같은 비선형 광고를 클라이언트 애플리케이션에 전달할 수 있지만 여전히 Primetime Ad Insertion을 사용하여 개별 광고 추적 URL을 전송하는 경우에도 가능합니다.
하이브리드 광고 추적을 활성화하려면 [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)의 `pttrackingmode` 매개 변수를 참조하십시오.
