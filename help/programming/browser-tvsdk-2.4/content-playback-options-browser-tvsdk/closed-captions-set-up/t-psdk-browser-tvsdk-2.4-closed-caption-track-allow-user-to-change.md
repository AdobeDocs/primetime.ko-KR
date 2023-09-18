---
description: 다음은 사용자가 자막 트랙을 선택하는 방법의 예입니다.
title: 사용자가 트랙을 변경할 수 있도록 허용
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# 사용자가 트랙을 변경할 수 있도록 허용{#allow-the-user-to-change-the-track}

다음은 사용자가 자막 트랙을 선택하는 방법의 예입니다.

1. 사용 가능한 자막 트랙을 표시하려면 `MediaPlayerItem.closedCaptionsTracks` 속성.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 현재 닫힌 캡션 트랙을 설정하려면 `MediaPlayerItem.selectClosedCaptionsTrack` 메서드를 사용합니다.
1. 미디어 플레이어 항목이 준비되면 를 사용하여 미디어 플레이어에서 검색합니다. ` MediaPlayer.  currentItem ` 메서드를 사용합니다.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
