---
description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
seo-description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
seo-title: 사용자 지정 컨텐츠 해결 프로그램 구현
title: 사용자 지정 컨텐츠 해결 프로그램 구현
uuid: 5f63cc1e-3f4b-460c-9151-2b9d364800e2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 사용자 지정 컨텐츠 해결 프로그램 구현 {#implement-a-custom-content-resolver}

기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.

TVSDK가 새 기회를 생성할 때 등록된 컨텐츠 해결자는 해당 기회를 해결할 수 있는 컨텐츠를 찾습니다. The first that return `true` is selected to resolve the opportunity. 컨텐츠 해결 프로그램이 없으면 해당 기회를 건너뜁니다. 컨텐츠 확인 프로세스는 일반적으로 비동기적이므로 컨텐츠 확인자는 프로세스가 완료되면 TVSDK에 알릴 책임이 있습니다.

1. 인터페이스를 확장하고 `ContentFactory`재정의하여 고유한 사용자 지정 `ContentFactory` 인터페이스를 구현할 수 `retrieveResolvers`있습니다.

   예:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
   
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   ```

1. 을 `ContentFactory` 에 `MediaPlayer`등록합니다.

   예:

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. 다음과 같이 객체를 TVSDK에 `AdvertisingMetadata` 전달합니다.
   1. 객체를 `AdvertisingMetadata` 만듭니다.
   1. 객체를 `AdvertisingMetadata` 저장할 `MediaPlayerItemConfig`위치.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. 클래스를 확장하는 사용자 지정 광고 해결 프로그램 클래스를 `ContentResolver` 만듭니다.
   1. 사용자 지정 광고 확인자에서 override `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`다음을 수행합니다.

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      전달된 `advertisingMetadata` 항목에서 다음 항목을 가져옵니다 `doConfigure`.

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. 각 배치 기회에 대해 를 `List<TimelineOperation>`만듭니다.

      이 샘플에서는 `TimelineOperation` 다음과 같은 구조를 `AdBreakPlacement`제공합니다.

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. 광고가 해결되면 다음 기능 중 하나를 호출합니다.

      * 광고 확인이 성공하면 `process(List<TimelineOperation> proposals)` `notifyCompleted(Opportunity opportunity)` 에 대한 `ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * 광고 해결에 실패하는 경우, `notifyResolveError``ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         예:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

이 샘플 사용자 지정 광고 확인자는 기회를 해결하고 간단한 광고를 제공합니다.

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 
```

