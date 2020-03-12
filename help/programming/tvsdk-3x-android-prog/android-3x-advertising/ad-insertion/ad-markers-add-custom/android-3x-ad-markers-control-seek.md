---
description: 사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.
seo-description: 사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.
seo-title: 사용자 정의 광고 마커 검색을 위한 재생 동작 제어
title: 사용자 정의 광고 마커 검색을 위한 재생 동작 제어
uuid: ec95a22f-0143-4c80-826f-d6b40e77cf26
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 사용자 정의 광고 마커 검색을 위한 재생 동작 제어 {#control-playback-behavior-for-seeking-over-custom-ad-markers}

사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.

기본적으로 사용자가 사용자 지정 광고 마커를 배치하여 발생하는 광고 섹션을 검색하거나 지난 경우 TVSDK는 광고를 건너뜁니다. 표준 광고 중단에 대한 현재 재생 동작과 다를 수 있습니다. 사용자가 하나 이상의 사용자 지정 광고를 지난 후 검색하는 경우 TVSDK를 설정하여 최근에 건너뛰었던 사용자 지정 광고의 시작 부분으로 재생 헤드의 위치를 변경할 수 있습니다.

1. 전화 `CustomRangeMetadata.setAdjustSeekPosition` 걸기 `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 에서 `customRangeMetadata` 사용합니다 `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
