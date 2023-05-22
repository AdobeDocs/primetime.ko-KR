---
description: OpportunityGenerator 클래스를 구현하여 고유한 Opportunity Generator를 구현할 수 있습니다.
title: 사용자 정의 영업 기회 생성기 구현
exl-id: 8fa97515-692c-4e34-9afb-17a5409228db
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# 사용자 정의 영업 기회 생성기 구현 {#implement-a-custom-opportunity-generator}

OpportunityGenerator 클래스를 구현하여 고유한 Opportunity Generator를 구현할 수 있습니다.

1. 사용자 정의 구현 `ContentFactory` 를 구현하여 `ContentFactory` 인터페이스 및 재정의 `retrieveGenerators`.

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

1. 등록 `ContentFactory` (으)로 `MediaPlayer`.

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

1. 다음을 구현하는 사용자 지정 영업 기회 생성기 클래스 만들기 `OpportunityGenerator` 클래스.

   ```java
   public class CustomOpportunityGenerator implements OpportunityGenerator  
   {...}
   ```

   1. 사용자 지정 영업 기회 생성기에서 `doConfigure`, `doUpdate` 및 `doCleanup`:

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

      시간 메타데이터를 가져오려면 다음을 수행합니다.

      ```java
      List<TimedMetadata> tList = getItem().getTimedMetadata(); 
      ```

   1. 각 `TimedMetadata` 또는 그룹 `TimedMetadata`, 다음 속성을 사용하여 기회를 만듭니다.

      ```java
      Opportunity( 
        String id,                      // Can be id from timedMetadata  
        Placement placementInformation, // Placement object containing Type, time, duration 
        Metadata metadataSettings,      // Ad metadata with targeting params sent to the ad provider 
        Metadata customParams           // Metadata for customizing resolving and/or tracking process. 
      ); 
      ```

   1. 생성된 각 영업 기회에 대해 `resolve` 다음에 있음 `OpportunityGeneratorClient:getClient().resolve(opportunity);`.

<!--<a id="example_7A46377EBE79458E87423EB95D0568D4"></a>-->

다음은 샘플 사용자 지정 배치 기회 감지기입니다.

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
