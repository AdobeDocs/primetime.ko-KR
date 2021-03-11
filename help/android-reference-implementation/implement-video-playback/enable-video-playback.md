---
description: HLS 스트림 설정 및 재생 작업을 처리하는 PlaybackManager를 만듭니다. 다른 구성은 필요하지 않습니다.
title: 비디오 재생 활성화
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 비디오 재생 활성화 {#enable-video-playback}

HLS 스트림 설정 및 재생 작업을 처리하는 PlaybackManager를 만듭니다. 다른 구성은 필요하지 않습니다.

1. 다음 코드가 [!DNL PlayerFragment.java]에 있는지 확인하여 미디어 플레이어 개체를 만듭니다.

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. `ManagerFactory`을 통해 재생 관리자를 만듭니다.

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 재생 이벤트를 처리하려면 `PlayerFragment`에서 `PlaybackManagerEventListener`을 구현합니다.

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. `PlayerFragment`에서 이벤트 리스너를 등록합니다.

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 비디오 리소스를 설정합니다.

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. `PlayerFragment`에서 제어 막대 작업을 설정합니다.

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 관련 API 설명서 {#related-api-documentation}

* [PlaybackManager 클래스](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)