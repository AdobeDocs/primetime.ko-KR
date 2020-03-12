---
description: TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAset의 availableMediaCharactersWithMediaSelectionOptionsAvailableNotification을 사용하여 플레이어 클라이언트에 알립니다.
seo-description: TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAset의 availableMediaCharactersWithMediaSelectionOptionsAvailableNotification을 사용하여 플레이어 클라이언트에 알립니다.
seo-title: 자막 노출
title: 자막 노출
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 자막 노출 {#expose-subtitles}

TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAset의 availableMediaCharactersWithMediaSelectionOptionsAvailableNotification을 사용하여 플레이어 클라이언트에 알립니다.

사용 가능한 자막은 `PTMediaPlayerItem` 속성 을 통해 액세스할 수 `subtitlesOptions`있습니다.

자막을 노출하려면

1. 클라이언트를 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 알림의 리스너로 등록합니다.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   클라이언트가 이 알림을 받으면 자막은 에 준비됩니다 `PTMediaPlayerItem`.
1. 다음 예와 유사한 `onMediaPlayerItemMediaSelectionOptionsAvailable` 메서드를 구현합니다.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   대체 오디오 트랙에 대한 자세한 내용은 대체 [오디오를 참조하십시오](../../alternate-audio/ios-3x-alternate-audio.md).