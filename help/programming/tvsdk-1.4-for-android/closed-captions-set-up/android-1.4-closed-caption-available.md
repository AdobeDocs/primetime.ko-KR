---
description: 폐쇄자막은 사운드가 들리지 않거나 뷰어가 잘 들리지 않을 때 비디오의 오디오 부분을 화면에 텍스트로 표시합니다.
seo-description: 폐쇄자막은 사운드가 들리지 않거나 뷰어가 잘 들리지 않을 때 비디오의 오디오 부분을 화면에 텍스트로 표시합니다.
seo-title: 사용 가능한 트랙 중에서 현재 캡션 트랙 선택
title: 사용 가능한 트랙 중에서 현재 캡션 트랙 선택
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용 가능한 트랙 중에서 현재 캡션 트랙 선택{#select-a-current-caption-track-from-among-available-tracks}

현재 사용 가능한 자막 트랙 목록에서 트랙을 선택할 수 있습니다. 가시성이 켜지면 표시되는 현재 트랙이 됩니다. 일부 트랙은 초기에 사용할 수 없으므로 더 많은 트랙을 사용할 수 있게 되었음을 나타내는 이벤트를 수신하십시오.

>[!TIP]
>
>자막은 항상 활성화되어 있습니다. 모든 기본 자막 트랙은 존재하는 것으로 간주됩니다. 기본 트랙(예: CC1-CC4, CS1-CS6)은 에서 열거됩니다 `ClosedCaptionsTrack.DefaultCCTypes`. 재생이 시작되면 TVSDK가 이러한 채널에서 활동을 찾습니다. 활동을 찾으면 해당 추적에 대한 `isActive` 메서드를 설정하고 `MediaPlayer.PlaybackEventListener.onUpdated` 이벤트를 전달합니다.

1. 미디어 플레이어가 준비된 상태 이상이어야 합니다.
1. 다음 이벤트에 대한 의견 수렴:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:자막 트랙의 초기 목록을 사용할 수 있습니다.

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
   
<b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b>selectedClosedCaptionsIndex = i;}}

```
1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

Retrieve the list each time that the event occurs to ensure that you always have the most current list.

