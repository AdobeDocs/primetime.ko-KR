---
description: 다음은 광고를 삭제하고 바꾸는 프로세스의 몇 가지 예입니다.
title: 광고 삭제 및 바꾸기 예제
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 광고 삭제 및 바꾸기 예제 {#examples-to-delete-and-replace-ads}

다음은 광고를 삭제하고 바꾸는 프로세스의 몇 가지 예입니다.

다음은 를 사용하는 예제입니다. `DELETE_RANGE`:

```java
// Assume that the 3 timerange specs are obtained through external means,  
// like a CMS. Assume mediaPlayer is an instance of a properly configured MediaPlayer 
// Use these 3 timerange specs to populate the RepaceTimeRange list 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, o)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.DELETE_RANGE); 
 
// create a MediaResource instance 
MediaResource mediaResource = ... ; 
 
// create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// prepare the content for playback by calling replaceCurrentResource  
mediaPlayer.replaceCurrentResource(mediaResource, config);
```

다음은 를 사용하는 예제입니다. `REPLACE_RANGE`:

```java
// Assume that the 3 timerange specs are obtained through external means, like 
//  a CMS. Assume mediaPlayer is an instance of a properly configured MediaPlayer 
// Use these 3 timerange specs to populate the RepaceTimeRange list 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 10000)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 20000)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 30000)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.REPLACE_RANGE); 
 
// create a MediaResource instance 
MediaResource mediaResource = ... ; 
 
// create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config = new MediaPlayerItemConfig(getActivity() 
    .getApplicationContext()); 
 
// Set Auditude settings, which are used for ad replacement, for this  
//  MediaPlayerItemConfig instance, 
 
... 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// prepare the content for playback by calling replaceCurrentResource 
mediaPlayer.replaceCurrentResource(mediaResource, config);
```
