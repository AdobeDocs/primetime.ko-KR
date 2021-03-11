---
description: 광고 확인 및 광고 로드는 사용자가 재생을 시작할 때까지 지연을 허용하지 않을 수 있습니다. 지연 광고 로드 해결 기능을 사용하면 시작 지연을 줄일 수 있습니다. 이제 광고를 중단 위치 전에 지정된 간격으로 광고를 확인할 수 있습니다. 이중 플레이어 접근 방식을 사용하여 이러한 목표를 달성할 수 있습니다.
title: 적시 광고 해결
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# 정시 광고 {#just-in-time-ad-resolving} 해결

광고 확인 및 광고 로드는 사용자가 재생을 시작할 때까지 지연을 허용하지 않을 수 있습니다. 지연 광고 로드 해결 기능을 사용하면 시작 지연을 줄일 수 있습니다. 이제 광고를 중단 위치 전에 지정된 간격으로 광고를 확인할 수 있습니다. 이중 플레이어 접근 방식을 사용하여 이러한 목표를 달성할 수 있습니다.

**기본 광고 해결 및 로드 프로세스:**

1. TVSDK는 매니페스트(재생 목록)를 다운로드하고 *는 모든 광고를 확인합니다.*
1. TVSDK *모든 광고를 로드하고 광고 세그먼트를 매니페스트에 올립니다.*
1. TVSDK는 플레이어를 준비된 상태로 이동시키고 컨텐츠 재생이 시작됩니다.

플레이어는 매니페스트에서 URL을 사용하여 광고 컨텐츠(크리에이티브)를 얻고 광고 컨텐츠가 TVSDK에서 재생할 수 있는 포맷인지 확인하고 TVSDK가 광고를 타임라인에 배치합니다. 광고를 확인하고 로드하는 이러한 기본 프로세스는 특히 매니페스트에 여러 개의 광고 URL이 포함되어 있는 경우, 사용자가 컨텐츠를 재생하기를 기다리는 동안 용납할 수 없는 긴 지연을 초래할 수 있습니다.

**지연 광고 해결:**

1. TVSDK가 재생 목록을 다운로드합니다.
1. TVSDK *모든 프리롤 광고를 확인 및 로드하고 플레이어를 PREMITED 상태로 이동하고 컨텐츠 재생이 시작됩니다.*
1. TVSDK *는 `PTAdMetadata::delayAdLoadingTolerance`에 정의된 값을 기준으로 광고 위치 이전 각 광고를 해결합니다.*

예를 들어 기본적으로 `delayAdLoadingTolerance`은 5초로 설정됩니다. AdBreak가 3:00에 재생되도록 설정된 경우 2:55:00에 해결됩니다. 광고 해상도가 5초 이상 걸린다고 생각되는 경우 이 값을 증가시킬 수 있습니다.

>[!IMPORTANT]
>
>**게으른 광고 해결 시 고려해야 할 요소:**
>* 지연 광고 해소는 SERVER_MAP 광고 신호 모드를 사용하는 VOD 스트림에 대해서만 지원됩니다.
>* 지연 광고 해제는 기본적으로 활성화되지 않습니다. 사용하려면 `PTAdMetadata::delayAdLoading` = YES를 설정해야 합니다.
>* [지연 광고 해결]은 [인스턴트 온] 기능과 호환되지 않습니다. 인스턴트 온에 대한 자세한 내용은 [인스턴트 온](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md)을 참조하십시오.
>* PIP(Picture-in-Picture) 모드는 레이지 광고 해결에서 지원되지 않습니다. 레이지 광고 해결을 활성화한 경우 모든 PIP(Picture-in-Picture) 모드를 비활성화하십시오.
>* 게으른 광고 해상도는 프리롤 광고에 영향을 주지 않습니다.

>


**게으른 광고 해결**

기존 레이지 광고 로드 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제는 비활성화됨).

광고 메타데이터를 설정할 때 `PTAdMetadata::delayAdLoading`= YES를 설정하여 지연 광고 해결을 활성화할 수 있습니다.

**지연 광고 해상도와 관련된 API:**

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
