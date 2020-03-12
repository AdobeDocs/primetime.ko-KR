---
description: 다음은 사용자가 자막 트랙을 선택하는 방법의 예입니다.
seo-description: 다음은 사용자가 자막 트랙을 선택하는 방법의 예입니다.
seo-title: 사용자가 트랙을 변경할 수 있도록 허용
title: 사용자가 트랙을 변경할 수 있도록 허용
uuid: bd3d4d20-9b52-4365-b656-83ec2a405a1c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 사용자가 트랙을 변경할 수 있도록 허용{#allow-the-user-to-change-the-track}

다음은 사용자가 자막 트랙을 선택하는 방법의 예입니다.

1. 사용 가능한 닫힌 캡션 트랙을 표시하려면 `MediaPlayerItem.closedCaptionsTracks` 속성을 사용합니다.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 현재 자막 트랙을 설정하려면 이 `MediaPlayerItem.selectClosedCaptionsTrack` 방법을 사용합니다.
1. 미디어 플레이어 항목을 준비한 후 ` MediaPlayer.  currentItem ` 방법을 사용하여 미디어 플레이어에서 검색합니다.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

