---
description: TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAsset의 availableMediaCharacteristicsWithMediaSelectionOptions에 대한 사용 가능 여부를 플레이어 클라이언트에 알립니다.
title: 자막 표시
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 자막 표시 {#expose-subtitles}

TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAsset의 availableMediaCharacteristicsWithMediaSelectionOptions에 대한 사용 가능 여부를 플레이어 클라이언트에 알립니다.

을 통해 사용 가능한 자막에 액세스할 수 있습니다. `PTMediaPlayerItem` 속성 `subtitlesOptions`.

자막을 표시하려면:

1. 클라이언트를 다음에 대한 리스너로 등록 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 알림입니다.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   클라이언트에서 이 알림을 받으면 다음에서 자막이 준비됩니다. `PTMediaPlayerItem`.
1. 구현 `onMediaPlayerItemMediaSelectionOptionsAvailable` 다음 예제와 유사한 메서드:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   대체 오디오 트랙에 대한 내용은  [대체 오디오](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).
