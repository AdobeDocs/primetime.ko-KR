---
description: TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAset의 availableMediaFeaturesWithMediaSelectionOptions의 가용성을 플레이어 클라이언트에 알립니다.
seo-description: TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAset의 availableMediaFeaturesWithMediaSelectionOptions의 가용성을 플레이어 클라이언트에 알립니다.
seo-title: 자막 노출
title: 자막 노출
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 자막 {#expose-subtitles} 노출

TVSDK는 PTMediaPlayerMediaSelectionOptionsAvailableNotification 알림을 사용하여 내부 AVAset의 availableMediaFeaturesWithMediaSelectionOptions의 가용성을 플레이어 클라이언트에 알립니다.

`PTMediaPlayerItem` 속성의 `subtitlesOptions`을 통해 사용 가능한 자막에 액세스할 수 있습니다.

자막을 노출하려면

1. `PTMediaPlayerMediaSelectionOptionsAvailableNotification` 알림의 리스너로 클라이언트를 등록합니다.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   클라이언트가 이 알림을 받으면 자막은 `PTMediaPlayerItem`에서 준비됩니다.
1. 다음 예제와 유사한 `onMediaPlayerItemMediaSelectionOptionsAvailable` 메서드를 구현합니다.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   대체 오디오 트랙에 대한 자세한 내용은 [대체 오디오](../../alternate-audio/ios-3x-alternate-audio.md)를 참조하십시오.