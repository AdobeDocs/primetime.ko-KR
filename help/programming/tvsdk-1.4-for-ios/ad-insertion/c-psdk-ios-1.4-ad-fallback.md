---
description: 폴백 규칙이 활성화된 VAST 파섹 VAST 파섹 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.
seo-description: 폴백 규칙이 활성화된 VAST 파섹 VAST 파섹 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.
seo-title: 광역 및 VMAP 광고를 위한 광고 폴백
title: 광역 및 VMAP 광고를 위한 광고 폴백
uuid: 290f0aeb-7314-4615-b477-24e65d5857ac
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 광역 및 VMAP 광고를 위한 광고 폴백 {#ad-fallback-for-vast-and-vmap-ads}

폴백 규칙이 활성화된 VAST 파섹 VAST 파섹 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.

VAST 파섹/VMAP(Digital Video Multiple Ad Playlist) 규격에서는 VAST 폴백이 활성화된 광고의 경우 빈 광고가 자동으로 폴백 광고 사용을 트리거한다고 명시합니다. VAST 광고가 비어 있는 경우 TVSDK는 폴백 광고 중 유효한 HLS 미디어 유형 대체를 찾습니다. 래퍼의 VAST 광고에 잘못된 미디어 유형이 있는 경우 TVSDK는 이 광고를 빈 것으로 취급합니다. TVSDK가 VMAP의 광고 인라인에 대해 동일해야 하는지 여부를 구성할 수 있습니다. VAST 기능에 대한 자세한 `fallbackOnNoAd` 내용은 VAST( [Digital Video Ad Serving Template) 3.0을 참조하십시오](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## VMAP 인라인 광고에 대한 대체 광고 동작 정의 {#section_D90BB3C6E539472EABF000C0F616DBE2}

VMAP 인라인 광고에 잘못된 미디어 유형이 들어 있는 경우 폴백을 활성화할 수 있습니다.

1. 선형/인라인 광고에 대한 미디어 유형이 HLS에 대해 올바르지 않을 때 VMAP이 뒤로 `FallbackOnInvalidCreativeEnabled` `YES` 넘어가도록 설정합니다.

   >[!NOTE]
   >
   >기본값은 NO입니다. 선형 광고가 잘못된 미디어 유형이나 광고를 다시 패키지할 수 없어 실패하는 경우 이 플래그를 사용하면 Primetime 광고 결정이 광고가 빈 VAST 래퍼인 것처럼 동일한 폴백 동작을 따를 수 있습니다.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## 광역 및 VMAP에 대한 광고 폴백 동작 {#section_5B6716CC49CC4C40964CFE9F122C57A6}

Primetime 광고 결정 시 비어 있거나 HLS에 대해 잘못된 미디어 유형이 있는 VAST 파섹 광고(크리에이티브)가 발견되면 대체 광고를 평가하여 반환할 내용을 결정합니다.

TVSDK에서 유효한 미디어 유형은 `application/x-mpegURL` (M3U8)뿐입니다.

독립 실행형 폴백(fallback) 광고가 있는 Primetime 광고 결정 플러그인은 다음 순서로 이러한 광고를 검사하고 유효한 미디어 유형이 있는 첫 번째 광고를 반환합니다.

1. 재패키징이 활성화되면 잘못된 미디어 유형의 광고가 처음 발생하는 것은 다른 잘못된 미디어 유형으로 처리됩니다.

   재패키징에 실패하면 이 프로세스는 광고의 추가 발생 시 적용됩니다.
1. TVSDK에서 올바른 폴백 광고를 찾지 못하면 잘못된 미디어 유형이 있는 원래 광고를 반환합니다.
1. 원본 광고 대신 유효한 MIME 유형의 폴백 광고가 반환되는 경우 Primetime 광고 의사 결정은 가능한 경우 오류 코드 403을 VAST 파섹 오류 URL로 보냅니다.
1. 대체 광고가 래퍼이고 여러 광고를 반환하는 경우 올바른 미디어 유형이 있는 광고만 반환됩니다.

>[!IMPORTANT]
>
>이 동작은 VAST 래퍼의 광고에 항상 활성화됩니다. VMAP의 VAST 광고 인라인인 경우 기본적으로 비헤이비어가 비활성화되지만 애플리케이션에서 활성화할 수 있습니다.

