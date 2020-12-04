---
description: 늦은 바인딩 오디오에서는 PTMediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-description: 늦은 바인딩 오디오에서는 PTMediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-title: 대체 오디오 트랙 액세스
title: 대체 오디오 트랙 액세스
uuid: 77e39633-bf17-4a06-a2a1-93fdaadedd17
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 대체 오디오 트랙 액세스{#access-alternate-audio-tracks}

늦은 바인딩 오디오에서는 PTMediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.

1. MediaPlayer가 적어도 `PTMediaPlayerStatusReady` 상태에 있을 때까지 기다립니다.
1. 이 이벤트에 대한 의견 수렴:

   알림 `PTMediaPlayerItemMediaSelectionOptionsAvailable`:오디오 트랙의 초기 목록을 사용할 수 있습니다.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. `PTMediaPlayerItem` 인스턴스에서 사용 가능한 오디오 트랙을 가져옵니다.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (선택 사항) 사용 가능한 트랙을 사용자에게 제공합니다.
1. `PTMediaPlayerItem` 인스턴스에서 선택한 오디오 트랙을 설정합니다.
