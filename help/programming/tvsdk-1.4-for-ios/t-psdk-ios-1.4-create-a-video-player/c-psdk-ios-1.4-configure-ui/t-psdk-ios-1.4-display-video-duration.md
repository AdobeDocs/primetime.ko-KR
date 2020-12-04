---
description: 현재 활성 컨텐츠의 기간을 표시할 수 있습니다.
seo-description: 현재 활성 컨텐츠의 기간을 표시할 수 있습니다.
seo-title: 비디오 지속 시간 표시
title: 비디오 지속 시간 표시
uuid: 02042070-9c55-4cbb-9dc1-49987451eb8f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 비디오 {#display-the-duration-of-the-video} 지속 시간 표시

현재 활성 컨텐츠의 기간을 표시할 수 있습니다.

다음 샘플 코드를 사용하여 비디오 지속 시간 표시를 구현합니다.

    &#39;PTMediaPlayer&#39; 속성 [seokableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)에 현재 검색 가능한 창 범위가 포함되어 있습니다.
    
    * VOD의 경우 이 범위는 광고를 포함한 전체 VOD 컨텐츠 범위입니다.
    * 라이브/리니어의 경우 이 범위는 검색 가능한 창을 나타냅니다.
    
    API에 대한 자세한 내용은 [TVSDK 1.4 for iOS API 참조](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)을 참조하십시오.

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
