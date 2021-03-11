---
description: 폴백 규칙을 사용하는 VAST(Digital Video Ad Serving Template) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하며 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.
keywords: 길이 광고;빈 광고
title: 광활한 VMAP 광고 대비 폴백
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# VAST 및 VMAP 광고에 대한 광고 폴백 {#ad-fallback-for-vast-and-vmap-ads}

폴백 규칙을 사용하는 VAST(Digital Video Ad Serving Template) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하며 대신 폴백 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.

VAST/Digital Video VMAP(Multiple Ad Playlist) 사양에는 VAST 폴백이 활성화된 광고의 경우 빈 광고가 자동으로 폴백 광고 사용을 트리거한다고 명시되어 있습니다. VAST 광고가 비어 있는 경우 TVSDK는 폴백 광고 중 유효한 HLS 미디어 유형 바꾸기를 찾습니다. 래퍼의 VAST 광고에 잘못된 미디어 유형이 있는 경우 TVSDK는 이 광고를 빈 것으로 취급합니다. TVSDK가 VMAP의 광고 인라인에서 동일해야 하는지 여부를 구성할 수 있습니다. VAST `fallbackOnNoAd` 기능에 대한 자세한 내용은 [VAST(디지털 비디오 광고 제공 템플릿) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)을 참조하십시오.

>[!NOTE]
>
>**제로 길이 광고**  - TV SDK에서 지속 시간이 0인 광고가 포함된 VAST 응답 또는 광고가 없는 광고 브레이크가 발견되면 길이가 0인 광고 중단에 대해 AD_BREAK_START / AD_BREAK_COMPLETE 이벤트를 실행합니다. *이 동작은 VOD 스트림에만 적용됩니다.* 앱이 SKIP 광고 정책을 사용하는 경우에도 TVSDK에서 이러한 이벤트를 실행합니다.
>
>TVSDK는 실시간 스트림에 대해 *NOT* NOT AD_BREAK_START / AD_BREAK_COMPLETE 이벤트를 실행하거나 사용자가 트릭플레이 또는 영길이 광고를 지나서 이동하려고 하는 경우를 수행합니다.