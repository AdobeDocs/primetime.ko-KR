---
description: 현재 활성화된 콘텐츠의 지속 시간을 표시할 수 있습니다.
title: 비디오 지속 시간 표시
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 비디오 지속 시간 표시 {#display-the-duration-of-the-video}

현재 활성화된 콘텐츠의 지속 시간을 표시할 수 있습니다.

다음 샘플 코드를 사용하여 비디오 지속 시간 표시를 구현합니다.

다음 `PTMediaPlayer` 속성, [검색 가능 범위](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange): 현재 검색 가능한 창 범위를 포함합니다.

* VOD의 경우 이 범위는 광고를 포함한 전체 VOD 콘텐츠 범위입니다.
* 라이브/선형의 경우 이 범위는 검색 가능한 창을 나타냅니다.

API에 대한 자세한 내용은 [iOS API 참조용 TVSDK 1.4](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
