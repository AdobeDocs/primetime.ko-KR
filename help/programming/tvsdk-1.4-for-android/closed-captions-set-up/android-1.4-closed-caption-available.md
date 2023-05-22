---
description: 자막을 닫으면 소리가 들리지 않거나 시청자가 듣기 어려울 때 비디오의 오디오 부분이 화면에 텍스트로 표시됩니다.
title: 사용 가능한 트랙 중에서 현재 캡션 트랙 선택
exl-id: 75970604-c318-4621-bad3-caab292c8a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 사용 가능한 트랙 중에서 현재 캡션 트랙 선택{#select-a-current-caption-track-from-among-available-tracks}

현재 사용 가능한 자막 트랙 목록에서 트랙을 선택할 수 있습니다. 이 트랙이 가시성이 켜져 있을 때 표시되는 현재 트랙이 됩니다. 일부 트랙은 처음에 사용할 수 없으므로 사용할 수 있게 되었음을 나타내는 이벤트를 수신합니다.

>[!TIP]
>
>폐쇄 캡션은 항상 활성화되어 있습니다. 모든 기본 자막 트랙은 존재하는 것으로 간주됩니다. 기본 트랙(예: CC1-CC4, CS1-CS6)은에서 열거됩니다. `ClosedCaptionsTrack.DefaultCCTypes`. 재생이 시작되면 TVSDK는 다음 채널에서 활동을 찾습니다. 활동을 찾으면 `isActive` 해당 추적 및 배포 방법 `MediaPlayer.PlaybackEventListener.onUpdated` 이벤트.

1. 미디어 플레이어가 적어도 준비됨 상태가 될 때까지 기다립니다.
1. 다음 이벤트를 수신합니다.

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: 자막 트랙의 초기 목록을 사용할 수 있습니다

1. 현재 사용 가능한 모든 자막 트랙 목록을 가져옵니다.

   예:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
         mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 사용 가능한 트랙을 현재 트랙으로 선택합니다.

   예:

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 더 많은 트랙을 사용할 수 있음을 나타내는 이벤트에 대한 리스너를 구현합니다. TVSDK가 이벤트를 전달하면 사용 가능한 트랙의 현재 목록을 검색합니다.

   이벤트가 발생할 때마다 목록을 검색하여 항상 최신 목록을 확보하십시오.
