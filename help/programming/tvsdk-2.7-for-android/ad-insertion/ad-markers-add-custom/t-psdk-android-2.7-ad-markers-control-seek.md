---
description: 사용자 지정 광고 마커를 사용할 때 TVSDK에서 광고를 찾는 방법에 대한 기본 동작을 재정의할 수 있습니다.
title: 사용자 지정 광고 마커를 통한 찾기를 위한 재생 비헤이비어 제어
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 사용자 지정 광고 마커를 통한 찾기를 위한 재생 비헤이비어 제어 {#control-playback-behavior-for-seeking-over-custom-ad-markers}

사용자 지정 광고 마커를 사용할 때 TVSDK에서 광고를 찾는 방법에 대한 기본 동작을 재정의할 수 있습니다.

기본적으로 사용자가 사용자 지정 광고 마커의 배치로 인해 발생하는 광고 섹션을 찾거나 지나가면 TVSDK가 광고를 건너뜁니다. 표준 광고 브레이크의 현재 재생 비헤이비어와 다를 수 있습니다. 사용자가 하나 이상의 사용자 지정 광고를 지나서 올 때 가장 최근에 건너뛴 사용자 지정 광고의 시작으로 플레이헤드의 위치를 조정하도록 TVSDK를 설정할 수 있습니다.

1. 호출 `CustomRangeMetadata.setAdjustSeekPosition` 포함 `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 사용 `customRangeMetadata` 위치: `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
