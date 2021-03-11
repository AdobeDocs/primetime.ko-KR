---
description: 현재 사용 가능한 자막 트랙 목록에서 트랙을 선택할 수 있습니다. 이 트랙은 현재 트랙이 되며, 이 트랙은 가시성이 설정되어 있을 때 표시됩니다. 일부 트랙은 처음에는 사용할 수 없으므로 더 많은 트랙을 사용할 수 있게 되었음을 나타내는 이벤트를 수신하십시오.
title: 사용 가능한 트랙 중에서 현재 캡션 트랙 선택
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# 사용 가능한 트랙 {#select-a-current-caption-track-from-among-available-tracks} 중에서 현재 캡션 트랙을 선택합니다.

현재 사용 가능한 자막 트랙 목록에서 트랙을 선택할 수 있습니다. 이 트랙은 현재 트랙이 되며, 이 트랙은 가시성이 설정되어 있을 때 표시됩니다. 일부 트랙은 처음에는 사용할 수 없으므로 더 많은 트랙을 사용할 수 있게 되었음을 나타내는 이벤트를 수신하십시오.

1. 미디어 플레이어가 `PREPARED` 상태 이상이어야 합니다.
1. 다음 이벤트에 대한 의견 수렴:

   * `MediaPlayerEvent.STATUS_CHANGED` 상태:  `MediaPlayerStatus.INITIALIZED`닫힌 캡션 트랙의 초기 목록을 사용할 수 있습니다.

1. 현재 사용 가능한 모든 자막 트랙 목록을 가져옵니다.

   예:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 현재 트랙으로 사용할 수 있는 트랙을 선택합니다.

   예:

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) {
        <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 더 많은 트랙을 사용할 수 있음을 나타내는 이벤트 리스너를 구현합니다. TVSDK가 이벤트를 전달하면 사용 가능한 트랙의 현재 목록을 검색합니다.

   이벤트가 발생할 때마다 목록을 검색하여 항상 최신 목록을 확인합니다.