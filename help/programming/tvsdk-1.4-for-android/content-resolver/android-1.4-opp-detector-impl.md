---
description: PlacementOpportunityDetector 인터페이스를 구현하여 고유한 영업 기회 감지기를 구현할 수 있습니다.
title: 사용자 정의 영업 기회 감지기 구현
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 사용자 정의 영업 기회 감지기 구현 {#implement-a-custom-opportunity-detector}

PlacementOpportunityDetector 인터페이스를 구현하여 고유한 영업 기회 감지기를 구현할 수 있습니다.

1. 사용자 지정 만들기 `AdvertisingFactory` 인스턴스 및 재정의 `createOpportunityDetector`. 예:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. 광고 클라이언트 팩터리를 `MediaPlayer`. 예:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 다음을 확장하는 사용자 정의 영업 기회 감지기 클래스 만들기 `PlacementOpportunityDetector` 클래스.
   1. 사용자 지정 영업 기회 감지기에서 이 함수를 재정의합니다.

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      다음 `timedMetadataList` 사용 가능한 목록 포함 `TimedMetadata`: 정렬됩니다. 메타데이터에는 광고 공급자에게 보낼 타겟팅 매개 변수와 사용자 지정 매개 변수가 포함되어 있습니다.

   1. 각 `TimedMetadata`, 만들기 `List<PlacementOpportunity>`. 목록은 비어 있을 수 있지만 null이 아닙니다. `PlacementOpportunity` 에는 다음 속성이 있어야 합니다.

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. 검색된 모든 시간 메타데이터 개체에 대해 배치 기회가 만들어지면 를 반환하면 됩니다. `PlacementOpportunity` 목록을 표시합니다.

다음은 샘플 사용자 지정 배치 기회 감지기입니다.

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 
```
