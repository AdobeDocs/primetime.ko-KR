---
description: TVSDK는 여러 개의 초기 PlacementInformation을 설정할 수 있습니다.
title: 여러 개의 초기 배치 정보
exl-id: 104e981e-7246-4e4a-9c14-dac6ee2624f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '20'
ht-degree: 0%

---

# 여러 개의 초기 배치 정보{#multiple-initial-placementinformations}

TVSDK는 여러 개의 초기 PlacementInformation을 설정할 수 있습니다.

```java
ArrayList<PlacementInformation> placementInformations = new ArrayList<PlacementInformation>(); 
CustomRangeHelper customRangeHelper = new CustomRangeHelper(mediaPlayerItem.getResource().getMetadata()); 
  
if (customRangeHelper.hasRanges() == null) { 
    if (adSignalingMode == AdSignalingMode.SERVER_MAP) { 
        placementInformations.add(new PlacementInformation(Type.SERVER_MAP, PlacementInformation.UNKNOWN_DURATION, 0)); 
    } else if (adSignalingMode == AdSignalingMode.MANIFEST_CUES) { 
        placementInformations.add(new PlacementInformation(Type.PRE_ROLL, timeMapping.getTime(), PlacementInformation.UNKNOWN_DURATION)); 
    } 
} 
else if (customRangeHelper.hasRanges() == CustomRangeHelper.MARK_RANGE) { 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.MARK, PlacementInformation.UNKNOWN_DURATION, 0)); 
} 
else if (customRangeHelper.hasRanges() == CustomRangeHelper.DELETE_RANGE) { 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.DELETE, PlacementInformation.UNKNOWN_DURATION, 0)); 
    if (adSignalingMode == AdSignalingMode.SERVER_MAP) { 
        placementInformations.add(new PlacementInformation(Type.SERVER_MAP,  
          PlacementInformation.UNKNOWN_DURATION, 0)); 
    } else if (adSignalingMode == AdSignalingMode.MANIFEST_CUES) { 
        placementInformations.add(new PlacementInformation(Type.PRE_ROLL,  
          timeMapping.getTime(), PlacementInformation.UNKNOWN_DURATION)); 
    } 
} 
else if (customRangeHelper.hasRanges() == CustomRangeHelper.REPLACE_RANGE) { 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.DELETE, PlacementInformation.UNKNOWN_DURATION, 0)); 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.REPLACE, PlacementInformation.UNKNOWN_DURATION, 0)); 
} 
return  placementInformations;
```
