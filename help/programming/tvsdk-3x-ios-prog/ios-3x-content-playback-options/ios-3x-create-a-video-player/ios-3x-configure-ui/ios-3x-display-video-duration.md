---
description: 현재 활성 상태인 컨텐츠의 기간을 표시할 수 있습니다.
title: 비디오 지속 시간을 표시합니다
exl-id: a41cb291-9355-44cf-80bb-9c3cf6628b81
source-git-commit: 85818281390b68522da2663496be025acf8f8675
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 비디오 지속 시간을 표시합니다 {#display-the-duration-of-the-video}

현재 활성 상태인 컨텐츠의 기간을 표시할 수 있습니다.

다음 샘플 코드를 사용하여 비디오 지속 시간 표시를 구현합니다.

다음 `PTMediaPlayer` property, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)에는 현재 표시되는 창 범위가 포함되어 있습니다.

* VOD의 경우 이 범위는 광고를 포함하여 전체 VOD 컨텐츠 범위입니다.
* 라이브/리니어의 경우 이 범위는 검색 가능한 창을 나타냅니다.

API에 대한 자세한 내용은 [iOS API용 TVSDK 3.4 참조](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
