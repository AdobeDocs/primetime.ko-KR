---
description: 기본 확인자를 기반으로 자체 콘텐츠 확인자를 구현할 수 있습니다.
title: 사용자 지정 콘텐츠 확인자 구현
exl-id: 04eff874-8a18-42f0-adb2-5b563e5c6a31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 사용자 지정 콘텐츠 확인자 구현 {#implement-a-custom-content-resolver}

기본 확인자를 기반으로 자체 콘텐츠 확인자를 구현할 수 있습니다.

TVSDK는 새 기회를 생성할 때 등록된 콘텐츠 해결자를 반복하여 해당 기회를 해결할 수 있는 기회를 찾습니다. 를 반환하는 첫 번째 `true` 영업 기회를 해결하기 위해 이(가) 선택됩니다. 콘텐츠 해결자를 사용할 수 없는 경우 해당 기회를 건너뜁니다. 콘텐츠 해결 프로세스는 일반적으로 비동기적이므로 프로세스가 완료되면 콘텐츠 해결자가 TVSDK에 알릴 책임이 있습니다.

1. 사용자 정의 구현 `ContentFactory`, 를 확장하여 `ContentFactory` 인터페이스 및 재정의 `retrieveResolvers`.

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

1. 등록 `ContentFactory` (으)로 `MediaPlayer`.

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

1. 전달 `AdvertisingMetadata` 다음과 같이 TVSDK에 개체를 추가합니다.
   1. 만들기 `AdvertisingMetadata` 개체.
   1. 저장 `AdvertisingMetadata` 대상 오브젝트 `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. 다음을 확장하는 사용자 지정 광고 해결 프로그램 클래스 만들기 `ContentResolver` 클래스.
   1. 사용자 지정 광고 해결자에서 재정의합니다. `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      다음을 이해합니다. `advertisingMetadata` 전달된 항목에서 `doConfigure`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. 각 배치 영업 기회에 대해 `List<TimelineOperation>`.

      이 샘플 `TimelineOperation` 다음에 대한 구조를 제공합니다. `AdBreakPlacement`:

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. 광고가 해결되면 다음 함수 중 하나를 호출합니다.

      * 광고 해결이 성공하면 을 호출합니다. `process(List<TimelineOperation> proposals)` 및 `notifyCompleted(Opportunity opportunity)` 다음에 있음 `ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * 광고 해결이 실패하면 `notifyResolveError` 다음에 있음 `ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         예:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

이 샘플 사용자 지정 광고 해결자는 기회를 해결하고 간단한 광고를 제공합니다.

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
