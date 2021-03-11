---
description: PlacementOpportunityDetector 인터페이스를 구현하여 고유한 기회 탐지기를 구현할 수 있습니다.
title: 사용자 정의 기회 탐지기 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 사용자 지정 기회 탐지 구현 {#implement-a-custom-opportunity-detector}

PlacementOpportunityDetector 인터페이스를 구현하여 고유한 기회 탐지기를 구현할 수 있습니다.

1. 사용자 지정 `AdvertisingFactory` 인스턴스를 만들고 `createOpportunityDetector`을(를) 재정의합니다. 예:

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

1. 광고 클라이언트 팩토리를 `MediaPlayer`에 등록합니다. 예:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. `PlacementOpportunityDetector` 클래스를 확장하는 사용자 지정 기회 탐지 클래스를 만듭니다.
   1. 사용자 지정 기회 탐지기에서 이 함수를 재정의합니다.

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      `timedMetadataList`에는 정렬되는 사용 가능한 `TimedMetadata` 목록이 포함되어 있습니다. 메타데이터에는 타깃팅 매개 변수와 광고 공급자에게 보낼 사용자 지정 매개 변수가 포함되어 있습니다.

   1. 각 `TimedMetadata`에 대해 `List<PlacementOpportunity>`을 만듭니다. 목록은 비워 둘 수 있지만 null은 아닙니다. `PlacementOpportunity` 에는 다음 속성이 있어야 합니다.

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. 감지된 모든 시간 메타데이터 객체에 대해 배치 기회가 만들어지면 `PlacementOpportunity` 목록을 반환하면 됩니다.

다음은 사용자 지정 배치 기회 탐지기의 예입니다.

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

