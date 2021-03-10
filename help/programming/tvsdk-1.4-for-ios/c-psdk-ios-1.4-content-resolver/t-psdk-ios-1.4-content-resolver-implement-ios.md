---
description: 기본 해상도에 따라 해상도를 구현할 수 있습니다.
title: 사용자 지정 기회/컨텐츠 해결 프로그램 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# 사용자 지정 기회/컨텐츠 확인자 구현{#implement-a-custom-opportunity-content-resolver}

기본 해상도에 따라 해상도를 구현할 수 있습니다.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. `PTContentResolver` 추상 클래스를 확장하여 사용자 지정 광고 확인자를 개발합니다.

   `PTContentResolver` 는 content resolver 클래스에서 구현해야 하는 인터페이스입니다. 같은 이름의 추상 클래스도 사용할 수 있으며, 구성을 자동으로 처리합니다(위임 가져오기).

   >[!TIP]
   >
   >`PTContentResolver` 는 클래스를 통해  `PTDefaultMediaPlayerClientFactory` 노출됩니다. 클라이언트는 `PTContentResolver` 추상 클래스를 확장하여 새 내용 확인자를 등록할 수 있습니다. 기본적으로, 특별히 제거하지 않는 한 `PTDefaultAdContentResolver`은 `PTDefaultMediaPlayerClientFactory`에 등록됩니다.

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
   
   @interface PTContentResolver : NSObject <PTContentResolver> 
   
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
   
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. `shouldResolveOpportunity`을(를) 구현하고 `YES`이 수신된 `PTPlacementOpportunity`를 처리해야 하는 경우 반환합니다.
1. 대체 내용 또는 광고 로드를 시작하는 `resolvePlacementOpportunity`을 구현합니다.
1. 광고가 로드되면 삽입할 컨텐트에 대한 정보가 있는 `PTTimeline`을 준비합니다.

       타임라인에 대한 유용한 정보는 다음과 같습니다.
   
   * 프리롤, 미드롤 및 포스트롤 유형의 `PTAdBreak`이 여러 개 있을 수 있습니다.

      * `PTAdBreak`의 값은 다음과 같습니다.

         * 시작 시간 및 중단 기간이 있는 `CMTimeRange`.

            이 속성은 `PTAdBreak`의 범위 속성으로 설정됩니다.

         * `NSArray` 의 `PTAd`를 참조하십시오.

            이 속성은 `PTAdBreak`의 광고 속성으로 설정됩니다.
   * `PTAd`은 광고를 나타내며 각 `PTAd`에는 다음 내용이 있습니다.

      * 광고의 기본 자산 속성으로 설정된 `PTAdHLSAsset`
      * 클릭 가능한 광고 또는 배너 광고로 여러 개의 `PTAdAsset` 인스턴스가 있을 수 있습니다.

   예:

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
   
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
   
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
   
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
   
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
   
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. `PTTimeline`을(를) 제공하는 `didFinishResolvingPlacementOpportunity`을(를) 호출합니다.
1. `registerContentResolver`을(를) 호출하여 사용자 정의 컨텐트/광고 확인자를 기본 미디어 플레이어 팩터리에 등록합니다.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. 사용자 지정 기회 해결 프로그램을 구현한 경우 기본 미디어 플레이어 팩터리에 등록합니다.

   >[!TIP]
   >
   >사용자 지정 컨텐츠/광고 해결 프로그램을 등록하려면 사용자 지정 기회 확인자를 등록하지 않아도 됩니다.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

플레이어가 컨텐츠를 로드하고 VOD 또는 LIVE 유형으로 판단되면 다음 중 하나가 발생합니다.>
* 컨텐츠가 VOD인 경우 사용자 정의 컨텐츠 확인자는 전체 비디오의 광고 타임라인을 가져오는 데 사용됩니다.
* 컨텐츠가 LIVE이면 컨텐츠에서 배치 기회(큐 포인트)가 검색될 때마다 사용자 지정 컨텐츠 확인자가 호출됩니다.
