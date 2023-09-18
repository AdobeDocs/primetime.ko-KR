---
description: 기본 확인자를 기반으로 확인자를 구현할 수 있습니다.
title: 사용자 지정 영업 기회/콘텐츠 해결사 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 사용자 지정 영업 기회/콘텐츠 해결사 구현 {#implement-a-custom-opportunity-content-resolver}

기본 확인자를 기반으로 확인자를 구현할 수 있습니다.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. 를 확장하여 사용자 지정 광고 해결자 개발 `PTContentResolver` 추상 클래스입니다.

   `PTContentResolver` 는 content resolver 클래스로 구현해야 하는 인터페이스입니다. 이름이 같은 추상 클래스도 사용할 수 있으며, 구성을 자동으로 처리합니다(위임자 가져오기).

   >[!TIP]
   >
   >`PTContentResolver` 을 통해 노출됩니다. `PTDefaultMediaPlayerClientFactory` 클래스. 클라이언트는 를 확장하여 새 콘텐츠 확인자를 등록할 수 있습니다. `PTContentResolver` 추상 클래스입니다. 기본적으로, 그리고 특별히 제거하지 않는 한 `PTDefaultAdContentResolver` 이(가)에 등록되어 있습니다. `PTDefaultMediaPlayerClientFactory`.

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

1. 구현 `shouldResolveOpportunity` 및 반환 `YES` 수신자를 처리해야 하는 경우 `PTPlacementOpportunity`.
1. 구현 `resolvePlacementOpportunity`: 대체 콘텐츠 또는 광고 로드를 시작합니다.
1. 광고가 로드된 후 다음을 준비합니다. `PTTimeline` 삽입할 콘텐츠에 대한 정보 포함

       다음은 타임라인에 대한 유용한 정보입니다.
   
   * 여러 개가 있을 수 있습니다. `PTAdBreak`s 프리롤, 미드롤 및 포스트롤 유형입니다.

      * A `PTAdBreak` 에는 다음이 포함되어 있습니다.

         * A `CMTimeRange` (시작 시간 및 브레이크 기간 포함)

           범위 속성으로 설정됩니다. `PTAdBreak`.

         * `NSArray` / `PTAd`s.

           의 광고 속성으로 설정됩니다. `PTAdBreak`.

   * A `PTAd` 는 광고를 나타내고, 각각은 `PTAd` 에는 다음이 포함되어 있습니다.

      * A `PTAdHLSAsset` 를 광고의 기본 자산 속성으로 설정합니다.
      * 아마도 복수 `PTAdAsset` 인스턴스: 클릭 가능한 광고 또는 배너 광고.

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

1. 호출 `didFinishResolvingPlacementOpportunity`, 다음을 제공합니다 `PTTimeline`.
1. 를 호출하여 사용자 지정 콘텐츠/광고 해결자를 기본 미디어 플레이어 팩토리에 등록합니다. `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. 사용자 지정 Opportunity Resolver를 구현한 경우 기본 미디어 플레이어 팩토리에 등록합니다.

   >[!TIP]
   >
   >사용자 지정 콘텐츠/광고 확인자를 등록하기 위해 사용자 지정 영업 기회 확인자를 등록할 필요가 없습니다.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

플레이어가 콘텐츠를 로드하고 VOD 또는 LIVE 유형이라고 판단되면 다음 중 하나가 발생합니다.

* 콘텐츠가 VOD인 경우 사용자 지정 콘텐츠 해결자를 사용하여 전체 비디오의 광고 타임라인을 가져옵니다.
* 콘텐츠가 라이브인 경우 콘텐츠에서 배치 기회(큐 포인트)가 감지될 때마다 사용자 지정 콘텐츠 확인자가 호출됩니다.
