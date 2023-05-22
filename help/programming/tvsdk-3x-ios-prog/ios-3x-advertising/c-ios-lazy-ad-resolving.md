---
description: 광고 해결 및 광고 로드로 인해 재생이 시작되기를 기다리는 사용자가 허용되지 않는 지연이 발생할 수 있습니다. 지연 광고 로드 해결 기능을 사용하면 이 시작 지연을 줄일 수 있습니다. 이제 광고 브레이크가 시작되기 전에 지정된 간격으로 광고를 확인할 수 있습니다. 이는 이중 플레이어 접근 방식을 사용하여 수행됩니다.
title: 적시 광고 해결
exl-id: dd5342c5-9f34-4778-a47a-91ff2eb03155
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 적시 광고 해결 {#just-in-time-ad-resolving}

광고 해결 및 광고 로드로 인해 재생이 시작되기를 기다리는 사용자가 허용되지 않는 지연이 발생할 수 있습니다. 지연 광고 로드 해결 기능을 사용하면 이 시작 지연을 줄일 수 있습니다. 이제 광고 브레이크가 시작되기 전에 지정된 간격으로 광고를 확인할 수 있습니다. 이는 이중 플레이어 접근 방식을 사용하여 수행됩니다.

**기본 광고 해결 및 로드 프로세스:**

1. TVSDK는 매니페스트(재생 목록) 및 *해결* 모든 광고.
1. TVSDK *로드* 모든 광고를 만들고 광고 세그먼트를 매니페스트에 결합합니다.
1. TVSDK가 플레이어를 PREPARED 상태로 이동하고 컨텐츠 재생이 시작됩니다.

플레이어는 매니페스트의 URL을 사용하여 광고 콘텐츠(크리에이티브)를 가져오고, 광고 콘텐츠가 TVSDK가 재생할 수 있는 포맷인지 확인하고, TVSDK가 타임라인에 광고를 배치합니다. 광고를 해결하고 로드하는 이러한 기본 프로세스로 인해 특히 매니페스트에 여러 광고 URL이 포함되어 있는 경우 콘텐츠 재생을 기다리는 사용자에게 허용될 수 없을 정도로 긴 지연이 발생할 수 있습니다.

**지연 광고 해결 중:**

1. TVSDK가 재생 목록을 다운로드합니다.
1. TVSDK *확인 및 로드* 프리롤 광고가 있으면 플레이어가 준비됨 상태로 이동되고 컨텐츠 재생이 시작됩니다.
1. TVSDK *해결* 각 광고는 다음에 정의된 값을 기준으로 해당 위치 이전에 중단됩니다. `PTAdMetadata::delayAdLoadingTolerance`.

예를 들어 기본적으로 `delayAdLoadingTolerance` 5초로 설정되어 있습니다. AdBreak를 3시에 재생하도록 설정하면 2시에 해결됩니다.:55:00. 광고 해상도가 5초 이상 소요될 것으로 예상되는 경우 이 값을 증가시킬 수 있습니다.

>[!IMPORTANT]
>
>**지연 광고 해결에서 고려해야 할 요소:**
>* 지연 광고 해결은 SERVER_MAP 광고 신호 모드 VOD 스트림에 대해서만 지원됩니다.
>* 지연 광고 해결은 기본적으로 활성화되어 있지 않습니다. 다음을 설정해야 합니다. `PTAdMetadata::delayAdLoading` = 활성화하려면 예.
>* 지연 광고 해결 기능은 인스턴트 온 기능과 호환되지 않습니다. 인스턴트 온에 대한 자세한 내용은 [즉시 사용](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* PIP(Picture-in-Picture) 모드는 지연 광고 해결에서 지원되지 않습니다. 지연 광고 해결을 활성화하는 경우 모든 화면 속 화면 모드를 비활성화하십시오.
>* 지연 광고 해결은 프리롤 광고에 영향을 주지 않습니다.
>

**지연 광고 해결 활성화**

기존 지연 광고 로드 메커니즘을 사용하여 지연 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(지연 광고 해결은 기본적으로 비활성화됨).

설정을 통해 지연 광고 해결을 활성화할 수 있습니다. `PTAdMetadata::delayAdLoading`= 광고 메타데이터를 설정할 때 예.

**지연 광고 해결과 관련된 API:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
