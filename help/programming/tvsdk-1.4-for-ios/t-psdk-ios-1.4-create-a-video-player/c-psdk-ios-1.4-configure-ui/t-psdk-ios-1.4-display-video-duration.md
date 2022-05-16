---
description: 현재 활성 상태인 컨텐츠의 기간을 표시할 수 있습니다.
title: 비디오 지속 시간을 표시합니다
exl-id: 4e31d784-4d16-470b-8317-11be32a55c2f
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 비디오 지속 시간을 표시합니다 {#display-the-duration-of-the-video}

현재 활성 상태인 컨텐츠의 기간을 표시할 수 있습니다.

다음 샘플 코드를 사용하여 비디오 지속 시간 표시를 구현합니다.

다음 `PTMediaPlayer` property, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)에는 현재 표시되는 창 범위가 포함되어 있습니다.

* VOD의 경우 이 범위는 광고를 포함하여 전체 VOD 컨텐츠 범위입니다.
* 라이브/리니어의 경우 이 범위는 검색 가능한 창을 나타냅니다.

API에 대한 자세한 내용은 [iOS API용 TVSDK 1.4 참조](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
