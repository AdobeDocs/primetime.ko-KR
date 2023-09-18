---
description: 대체 규칙이 활성화된 VAST(디지털 비디오 광고 제공 템플릿) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 대체 광고를 사용합니다. 대체 동작의 몇 가지 측면을 구성할 수 있습니다.
keywords: 길이가 0인 광고;빈 광고
title: VAST 및 VMAP 광고에 대한 광고 대체
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# VAST 및 VMAP 광고에 대한 광고 대체 {#ad-fallback-for-vast-and-vmap-ads}

대체 규칙이 활성화된 VAST(디지털 비디오 광고 제공 템플릿) 광고(또는 크리에이티브)의 경우 TVSDK는 잘못된 미디어 유형의 광고를 빈 광고로 취급하고 대신 대체 광고를 사용합니다. 대체 동작의 몇 가지 측면을 구성할 수 있습니다.

VAST/Digital Video Multiple Ad Playlist (VMAP) 사양에는 VAST 폴백이 활성화된 광고의 경우 빈 광고가 자동으로 폴백 광고 사용을 트리거한다고 나와 있습니다. VAST 광고가 비어 있는 경우, TVSDK는 대체 대체 대체 대체 대체 HLS 광고를 찾습니다. 래퍼의 VAST 광고에 잘못된 미디어 유형이 있는 경우 TVSDK는 이 광고를 비어 있는 것으로 처리합니다. VMAP에서 인라인된 광고에 대해 TVSDK가 동일한 작업을 수행할지 여부를 구성할 수 있습니다. VAST에 대한 자세한 정보 `fallbackOnNoAd` 기능, 참조 [디지털 비디오 광고 서비스 제공 템플릿(VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**길이가 0인 광고** - TVSDK에서 지속 시간이 0인 광고가 포함된 VAST 응답이나 광고가 없는 광고 브레이크가 발생하면 해당 빈 광고 브레이크에 대해 AD_BREAK_START / AD_BREAK_COMPLETE 이벤트가 실행됩니다. *이 동작은 VOD 스트림에만 적용됩니다.* TVSDK는 앱에서 광고 건너뛰기 정책을 사용하는 경우에도 이러한 이벤트를 실행합니다.
>
>TVSDK는 *아님* 라이브 스트림에 대한 AD_BREAK_START / AD_BREAK_COMPLETE 이벤트를 실행하거나 사용자가 트리크플레이를 사용하거나 길이가 0인 광고를 지나가려고 할 때 발생합니다.
