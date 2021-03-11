---
description: TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAsset의 availableMediaCharactersWithMediaSelectionOptionsAvailableNotification을 사용하여 플레이어 클라이언트에 알립니다.
title: 자막 노출
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 자막 표시 {#expose-subtitles}

TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAsset의 availableMediaCharactersWithMediaSelectionOptionsAvailableNotification을 사용하여 플레이어 클라이언트에 알립니다.

`PTMediaPlayerItem` 속성의 `subtitlesOptions`을 통해 사용 가능한 자막에 액세스할 수 있습니다.

자막을 노출하려면

1. 클라이언트를 `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 알림의 리스너로 등록합니다.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   클라이언트가 이 알림을 받으면 자막이 `PTMediaPlayerItem`에서 준비됩니다.
1. 다음 예제와 유사한 `onMediaPlayerItemMediaSelectionOptionsAvailable` 메서드를 구현합니다.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   대체 오디오 트랙에 대한 자세한 내용은 [대체 오디오](../../alternate-audio/ios-3x-alternate-audio.md)를 참조하십시오.