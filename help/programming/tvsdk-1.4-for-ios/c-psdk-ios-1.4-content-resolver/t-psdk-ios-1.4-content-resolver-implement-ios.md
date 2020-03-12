---
description: 기본 해상도에 따라 해상도를 구현할 수 있습니다.
seo-description: 기본 해상도에 따라 해상도를 구현할 수 있습니다.
seo-title: 사용자 지정 기회/컨텐츠 해결 프로그램 구현
title: 사용자 지정 기회/컨텐츠 해결 프로그램 구현
uuid: bfc14318-ca4b-46cc-8128-e3743af06d9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 지정 기회/컨텐츠 해결 프로그램 구현{#implement-a-custom-opportunity-content-resolver}

기본 해상도에 따라 해상도를 구현할 수 있습니다.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. 추상 클래스를 확장하여 사용자 지정 광고 해결 프로그램을 `PTContentResolver` 개발합니다.

   `PTContentResolver` 는 컨텐츠 해결 프로그램 클래스에서 구현해야 하는 인터페이스입니다. 같은 이름의 추상 클래스를 사용할 수 있으며, 위임 가져오기를 사용하여 구성을 자동으로 처리합니다.

   >[!TIP]
   >
   >`PTContentResolver` 이 `PTDefaultMediaPlayerClientFactory` 클래스를 통해 노출됩니다. 클라이언트는 `PTContentResolver` 추상 클래스를 확장하여 새 컨텐츠 해결 프로그램을 등록할 수 있습니다. 기본적으로, 그리고 구체적으로 제거하지 않는 한, 는 `PTDefaultAdContentResolver` 에 등록되어 `PTDefaultMediaPlayerClientFactory`있습니다.

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

1. 수신한 내용을 처리해야 `shouldResolveOpportunity` 하는 경우 구현하고 `YES` `PTPlacementOpportunity`반환합니다.
1. 대체 컨텐츠 또는 광고 로드를 시작하는 구현 `resolvePlacementOpportunity`.
1. 광고가 로드되면 삽입할 컨텐트에 대한 정보가 `PTTimeline` 포함된 내용을 준비합니다.

       다음은 타임라인에 대한 유용한 정보입니다.
   
   * 프리롤, 미드롤 및 포스트롤 유형의 `PTAdBreak`여러 가지가 있을 수 있습니다.

      * A `PTAdBreak` 에는 다음이 포함됩니다.

         * 시작 `CMTimeRange` 시간과 휴식 기간이 있는 A.

            이것은 의 범위 속성으로 `PTAdBreak`설정됩니다.

         * `NSArray` 의 `PTAd`두 개.

            이것은 광고 속성으로 `PTAdBreak`설정됩니다.
   * A `PTAd` 는 광고를 나타내며 각 `PTAd` 광고에는 다음이 포함됩니다.

      * 광고의 기본 자산 속성으로 `PTAdHLSAsset` 설정된 경우입니다.
      * 클릭 가능한 광고 또는 배너 광고와 같은 여러 `PTAdAsset` 인스턴스가 있을 수 있습니다.
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

1. Call `didFinishResolvingPlacementOpportunity`을 참조하십시오 `PTTimeline`.
1. 사용자 지정 컨텐츠/광고 확인자를 기본 미디어 플레이어 팩터리에 등록하려면 `registerContentResolver`전화하십시오.

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
   >사용자 지정 컨텐츠/광고 확인자를 등록하려면 사용자 지정 기회 확인자를 등록하지 않아도 됩니다.

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
* 컨텐츠가 VOD인 경우 사용자 지정 컨텐츠 확인자는 전체 비디오의 광고 타임라인을 가져오는 데 사용됩니다.
* 컨텐츠가 LIVE이면 사용자 지정 컨텐츠 확인자는 컨텐츠에서 배치 기회(큐 포인트)가 검색될 때마다 호출됩니다.
