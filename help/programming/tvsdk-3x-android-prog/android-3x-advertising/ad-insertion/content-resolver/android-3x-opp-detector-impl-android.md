---
description: OpportunityGenerator 클래스를 구현하여 고유한 기회 생성기를 구현할 수 있습니다.
seo-description: OpportunityGenerator 클래스를 구현하여 고유한 기회 생성기를 구현할 수 있습니다.
seo-title: 사용자 정의 기회 생성기 구현
title: 사용자 정의 기회 생성기 구현
uuid: 6a6a6aa4-51f8-4e3c-9255-d87b488b820d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# 사용자 지정 기회 생성기 {#implement-a-custom-opportunity-generator} 구현

OpportunityGenerator 클래스를 구현하여 고유한 기회 생성기를 구현할 수 있습니다.

1. `ContentFactory` 인터페이스를 구현하고 `retrieveGenerators`을(를) 재정의하여 사용자 지정 `ContentFactory`을 구현합니다.

   예:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
           List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
           generators.add(MyOpportunityGenerator(item)); 
           return generators; 
       } 
       ... 
   }
   ```

1. `ContentFactory`을 `MediaPlayer`에 등록합니다.

   예:

   ```java
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. `OpportunityGenerator` 클래스를 구현하는 사용자 지정 기회 생성기 클래스를 만듭니다.

   ```java
   public class CustomOpportunityGenerator implements OpportunityGenerator  
   {...}
   ```

   1. 사용자 지정 기회 생성기에서 `doConfigure`, `doUpdate` 및 `doCleanup`를 무시합니다.

      ```java
      @Override 
       public void configure(MediaPlayerItem item, Context context,  
       OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
      
      protected void update(long playhead, TimeRange playbackRange){ 
      } 
      
      protected void cleanup(){ 
      }
      ```

      시간 메타데이터를 얻으려면 다음을 수행하십시오.

      ```java
      List<TimedMetadata> tList = getItem().getTimedMetadata(); 
      ```

   1. 각 `TimedMetadata` 또는 `TimedMetadata` 그룹에 대해 다음 특성을 가진 기회를 만듭니다.

      ```java
      Opportunity( 
        String id,                      // Can be id from timedMetadata  
        Placement placementInformation, // Placement object containing Type, time, duration 
        Metadata metadataSettings,      // Ad metadata with targeting params sent to the ad provider 
        Metadata customParams           // Metadata for customizing resolving and/or tracking process. 
      ); 
      ```

   1. 만들어진 각 기회에 대해 `OpportunityGeneratorClient:getClient().resolve(opportunity);`에서 `resolve`을(를) 호출합니다.

<!--<a id="example_7A46377EBE79458E87423EB95D0568D4"></a>-->

사용자 지정 배치 기회 탐지기 샘플입니다.

```java
public class MyOpportunityGenerator implements OpportunityGenerator {

     @Override 
      public void configure(MediaPlayerItem item, Context context,  
      OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
 
        MediaPlayerItem item = getItem(); 
        MediaPlayerItemConfig itemConfig = item.getConfig(); 
 
        if (itemConfig == null || itemConfig.getAdvertisingMetadata() == null) { 
            // no ad metadata, no ads 
            return; 
        } 
 
        AdvertisingMetadata metadata = item.getConfig().getAdvertisingMetadata();

        AdSignalingMode mode = itemConfig.getAdSignalingMode(); 
 
        if (mode == AdSignalingMode.CUSTOM_RANGES) 
        { 
            // don't override custom ad ranges 
            return; 
        } 
 
        Placement.Type pType = (mode == AdSignalingMode.MANIFEST_CUES) ?  
                  Placement.Type.PRE_ROLL : Placement.Type.SERVER_MAP; 
        Placement.Mode pMode = Placement.Mode.DEFAULT; 
        Placement placement = new Placement(pType, playhead,  
                  Placement.UNKNOWN_DURATION, pMode); 
 
        Opportunity opportunity = new Opportunity("initialOpportunity", placement,  
                  metadata, null); 
 
        OpportunityGeneratorClient client = getClient(); 
        client.resolve(opportunity); 
    } 
 
    @Override 
    protected void update(long playhead, TimeRange playbackRange) { 
 
 ... 
 timedMetadataList = getItem().getTimedMetadata(); 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
         if (isOpportunity(timedMetadata)) {   // check if given timedMetadata should  
                                               // be considered as an opportunity 
  // create a PlacementOpportunity object and add it to the opportunities list 
                Opportunity opportunity = new Opportunity("id", placement, metadata, null); 
                client.resolve(opportunity) 
          } 
        } 
    } 
 
    @Override 
    protected void cleanup() {} 
}
```
