---
description: 여러 컨텐츠 해상도를 사용하여 서로 다른 타임라인 작업을 처리할 수 있습니다.
seo-description: 여러 컨텐츠 해상도를 사용하여 서로 다른 타임라인 작업을 처리할 수 있습니다.
seo-title: 광고 삭제/바꾸기 컨텐츠 해상도
title: 광고 삭제/바꾸기 컨텐츠 해상도
uuid: ed168c52-ab7b-4fe6-8775-eb18018dc249
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 광고 삭제/바꾸기 컨텐츠 해상도 {#content-resolvers-for-ad-deletion-replacement}

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

