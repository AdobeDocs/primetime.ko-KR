---
description: 사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.
title: 사용자 정의 광고 마커 검색을 위한 재생 동작 제어
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 사용자 지정 광고 마커 {#control-playback-behavior-for-seeking-over-custom-ad-markers}에 대한 검색을 위한 재생 동작 제어

사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.

기본적으로 사용자가 사용자 지정 광고 마커 배치로 인해 발생하는 광고 섹션을 검색하거나 지나치면 TVSDK는 광고를 건너뜁니다. 표준 광고 중단에 대한 현재 재생 비헤이비어와 다를 수 있습니다. 사용자가 하나 이상의 사용자 지정 광고를 지난 후 검색하는 경우 TV SDK를 설정하여 최근에 건너뛴 사용자 지정 광고 시작 부분으로 재생 헤드의 위치를 변경할 수 있습니다.

1. `true`을(를) 사용하여 `CustomRangeMetadata.setAdjustSeekPosition`을(를) 호출합니다.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. `MediaPlayerItemConfig`에서 `customRangeMetadata`을 사용합니다.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```

