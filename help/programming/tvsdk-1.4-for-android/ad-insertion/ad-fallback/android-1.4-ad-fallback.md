---
description: 대체 규칙이 활성화된 VAST(디지털 비디오 광고 제공 템플릿) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 대체 광고를 사용합니다. 대체 동작의 몇 가지 측면을 구성할 수 있습니다.
title: VAST 및 VMAP 광고에 대한 광고 대체
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# VAST 및 VMAP 광고에 대한 광고 대체 {#ad-fallback-for-vast-and-vmap-ads}

대체 규칙이 활성화된 VAST(디지털 비디오 광고 제공 템플릿) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 대체 광고를 사용합니다. 대체 동작의 몇 가지 측면을 구성할 수 있습니다.

VAST/Digital Video Multiple Ad Playlist (VMAP) 사양에는 VAST 폴백이 활성화된 광고의 경우 빈 광고가 자동으로 폴백 광고 사용을 트리거한다고 나와 있습니다. VAST 광고가 비어 있는 경우, TVSDK는 대체 대체 대체 대체 대체 HLS 광고를 찾습니다. 래퍼의 VAST 광고에 잘못된 미디어 유형이 있는 경우 TVSDK는 이 광고를 비어 있는 것으로 처리합니다. VMAP에서 인라인된 광고에 대해 TVSDK가 동일한 작업을 수행할지 여부를 구성할 수 있습니다. VAST에 대한 자세한 정보 `fallbackOnNoAd` 기능, 참조 [디지털 비디오 광고 서비스 제공 템플릿(VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## VMAP 인라인 광고에 대한 대체 광고 동작 정의 {#define-fallback-ad-behavior-for-vmap-inline-ads}

VMAP 인라인 광고에 잘못된 미디어 유형이 포함된 경우 폴백을 설정할 수 있습니다.

1. 설정 `setFallbackOnInvalidCreativeEnabled` 끝 `true` 선형/인라인 광고의 미디어 유형이 HLS에 유효하지 않을 때 VMAP이 폴백되도록 합니다.

   기본값은 false입니다. 선형 광고가 유효하지 않은 미디어 유형을 가지고 있거나 광고를 다시 패키징할 수 없기 때문에 실패하는 경우, 이 플래그를 사용하면 Primetime 광고 의사 결정이 광고가 빈 VAST 래퍼인 것처럼 동일한 폴백 동작을 따를 수 있습니다.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

## VAST 및 VMAP에 대한 광고 대체 동작 {#ad-fallback-behavior-for-vast-and-vmap}

Primetime 광고 의사 결정에 비어 있거나 HLS에 유효하지 않은 미디어 유형을 가진 VAST 광고(크리에이티브)가 발생하면 대체 광고를 평가하여 반환할 항목을 결정합니다.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

TVSDK에서 유효한 미디어 유형은 다음과 같습니다. `application/x-mpegURL` (M3U8).

독립형 대체 광고가 있는 경우, Primetime 광고 의사 결정 플러그인은 다음 순서로 이러한 광고를 검사하고 유효한 미디어 유형의 첫 번째 광고를 반환합니다.

1. 리패키징이 활성화되면 잘못된 미디어 유형의 광고가 처음 발생하는 경우 다른 잘못된 미디어 유형과 유사하게 처리됩니다.

   다시 패키징에 실패하는 경우 이 프로세스는 추가 광고 발생 횟수에 적용됩니다.
1. TVSDK에서 유효한 대체 광고를 찾지 못하면 잘못된 미디어 유형의 원래 광고가 반환됩니다.
1. 유효한 MIME 유형의 대체 광고가 원본 광고 대신 반환되는 경우, Primetime ad decisioning은 오류 코드 403을 VAST 오류 URL로 보냅니다(사용 가능한 경우).
1. 대체 광고가 래퍼이고 여러 광고를 반환하는 경우 올바른 미디어 유형의 광고만 반환됩니다.

>[!IMPORTANT]
>
>이 동작은 VAST 래퍼의 광고에 대해 항상 활성화되어 있습니다. VMAP에서 인라인된 VAST 광고의 경우, 기본적으로 비헤이비어는 비활성화되지만 애플리케이션에서 활성화할 수 있습니다.
