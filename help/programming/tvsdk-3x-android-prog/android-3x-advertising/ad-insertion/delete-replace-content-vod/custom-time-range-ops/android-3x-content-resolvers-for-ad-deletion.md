---
description: 여러 컨텐츠 해상도를 사용하여 서로 다른 타임라인 작업을 처리할 수 있습니다.
seo-description: 여러 컨텐츠 해상도를 사용하여 서로 다른 타임라인 작업을 처리할 수 있습니다.
seo-title: 광고 삭제/교체를 위한 컨텐츠 해상도
title: 광고 삭제/교체를 위한 컨텐츠 해상도
uuid: d43d54be-e04a-49dd-a695-e4e8f981ccb4
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# 광고 삭제/교체 {#content-resolvers-for-ad-deletion-replacement} 컨텐츠 해상도

여러 컨텐츠 해상도를 사용하여 서로 다른 타임라인 작업을 처리할 수 있습니다.

```java
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
    List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
    MediaPlayerItemConfig itemConfig = item.getConfig(); 
    if(itemConfig) { 
        CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
        if (customRanges) { 
            List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
 
            if (timeRanges && timeRanges.size() > 0) { 
                //CustomRangeResolver is activated by the presence of CustomRanges 
                resolvers.add(new CustomRangeResolver()); 
            } 
        } 
        AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
        if (metadata) { 
            if (metadata instanceOf AuditudeSettings)  
            resolvers.add(new AuditudeResolver(getContext());                                      
        } 
    } 
    //Add your custom resolver if any 
    resolvers.add(MyOpportunityGenerator(item)); 
    return resolvers; 
} 
```
