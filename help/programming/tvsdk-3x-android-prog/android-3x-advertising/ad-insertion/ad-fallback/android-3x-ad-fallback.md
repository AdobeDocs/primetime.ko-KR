---
description: 폴백 규칙이 활성화된 VAST 파섹 VAST 파섹 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.
keywords: zero length ad;empty ad
seo-description: 폴백 규칙이 활성화된 VAST 파섹 VAST 파섹 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.
seo-title: 광역 및 VMAP 광고를 위한 광고 폴백
title: 광역 및 VMAP 광고를 위한 광고 폴백
uuid: 688f0b67-9f5b-4c21-ab33-86d21580fbe9
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 광역 및 VMAP 광고를 위한 광고 폴백 {#ad-fallback-for-vast-and-vmap-ads}

폴백 규칙이 활성화된 VAST 파섹 VAST 파섹 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.

VAST 파섹/VMAP(Digital Video Multiple Ad Playlist) 사양은 VAST 폴백이 활성화된 광고의 경우 빈 광고가 자동으로 폴백 광고 사용을 트리거한다고 명시합니다. VAST 광고가 비어 있는 경우 TVSDK는 폴백 광고 중 유효한 HLS 미디어 유형 대체를 찾습니다. 래퍼의 VAST 광고에 잘못된 미디어 유형이 있는 경우 TVSDK는 이 광고를 빈 것으로 취급합니다. TVSDK가 VMAP의 광고 인라인에 대해 동일해야 하는지 여부를 구성할 수 있습니다. VAST 기능에 대한 자세한 `fallbackOnNoAd` 내용은 VAST( [Digital Video Ad Serving Template) 3.0을 참조하십시오](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**제로 길이 광고** - TVSDK에서 지속 시간이 0인 광고가 포함된 VAST 응답이나 광고가 없는 광고 브레이크가 발생하는 경우 이러한 제로 길이 광고 브레이크에 대해 AD_BREAK_START / AD_BREAK_COMPLETE 이벤트가 발생합니다. *이 동작은 VOD 스트림에만 적용됩니다.* 앱이 SKIP 광고 정책을 사용하는 경우에도 TVSDK에서 이러한 이벤트를 실행합니다.
>
>TVSDK에서는 라이브 스트림에 대해 AD_BREAK_START/AD_BREAK_COMPLETE 이벤트를 실행하거나 사용자가 트릭플레이를 사용하거나 제로 길이의 광고를 지나 시도할 때 실행되지 *않습니다* .