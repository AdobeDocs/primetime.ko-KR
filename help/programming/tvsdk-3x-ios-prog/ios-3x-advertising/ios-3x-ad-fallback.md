---
description: 폴백 규칙을 사용하는 VAST(Digital Video Ad Serving Template) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하며 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.
title: 광활한 VMAP 광고 대비 폴백
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# VAST 및 VMAP 광고에 대한 광고 폴백 {#ad-fallback-for-vast-and-vmap-ads}

폴백 규칙을 사용하는 VAST(Digital Video Ad Serving Template) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하며 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.

VAST/Digital Video VMAP(Multiple Ad Playlist) 사양에는 VAST 폴백이 활성화된 광고의 경우 빈 광고가 자동으로 폴백 광고 사용을 트리거한다고 명시되어 있습니다. VAST 광고가 비어 있는 경우 TVSDK는 폴백 광고 중 유효한 HLS 미디어 유형 바꾸기를 찾습니다. 래퍼의 VAST 광고에 잘못된 미디어 유형이 있는 경우 TVSDK는 이 광고를 빈 것으로 취급합니다. TVSDK가 VMAP의 광고 인라인에서 동일해야 하는지 여부를 구성할 수 있습니다. VAST `fallbackOnNoAd` 기능에 대한 자세한 내용은 [VAST(디지털 비디오 광고 제공 템플릿) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)을 참조하십시오.

## VMAP 인라인 광고 {#section_D90BB3C6E539472EABF000C0F616DBE2}에 대한 대체 광고 비헤이비어 정의

VMAP 인라인 광고에 잘못된 미디어 유형이 포함되어 있으면 폴백을 활성화할 수 있습니다.

1. 선형/인라인 광고에 대한 미디어 유형이 HLS에 대해 유효하지 않을 때 VMAP이 뒤로 돌아가도록 `FallbackOnInvalidCreativeEnabled`을(를) `YES`으로 설정합니다.

   >[!NOTE]
   >
   >기본값은 NO입니다. 선형 광고가 잘못된 미디어 유형이거나 광고를 다시 패키지화할 수 없기 때문에 실패하는 경우, 이 플래그를 통해 Primetime 광고 결정이 광고가 빈 VAST 래퍼인 것처럼 동일한 폴백 동작을 따를 수 있습니다.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## VAST 및 VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}에 대한 광고 폴백 동작

Primetime 광고 결정 시 비어 있거나 HLS에 유효하지 않은 미디어 유형이 있는 VAST 광고(크리에이티브)가 발견되면 반환할 광고를 평가하여 확인할 수 있습니다.

TVSDK에서 유효한 미디어 유형은 `application/x-mpegURL`(M3U8)뿐입니다.

독립 실행형 폴백 광고가 있는 경우 Primetime 광고 결정 플러그인은 다음 순서로 이러한 광고를 검토하고 올바른 미디어 유형이 있는 첫 번째 광고를 반환합니다.

1. 재패키징이 활성화되면 미디어 유형이 잘못된 광고의 첫 번째 발생을 다른 잘못된 미디어 유형으로 취급합니다.

   재패키징에 실패하면 이 프로세스는 광고의 추가 발생 시 적용됩니다.
1. TVSDK에서 유효한 대체 광고를 찾을 수 없으면 잘못된 미디어 유형의 원래 광고를 반환합니다.
1. 원본 광고 대신 유효한 MIME 유형의 대체 광고가 반환되는 경우 Primetime 광고 결정 기능에서는 오류 코드 403을 VAST 오류 URL로 보냅니다(가능한 경우).
1. 대체 광고가 래퍼이고 여러 광고를 반환하는 경우 올바른 미디어 유형이 있는 광고만 반환됩니다.

>[!IMPORTANT]
>
>이 비헤이비어는 VAST 래퍼의 광고에 대해 항상 활성화되어 있습니다. VMAP의 VAST 광고 인라인에서는 기본적으로 비헤이비어가 비활성화되지만 응용 프로그램에서 이를 활성화할 수 있습니다.