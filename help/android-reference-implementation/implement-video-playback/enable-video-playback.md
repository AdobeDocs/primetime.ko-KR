---
description: HLS 스트림 설정 및 재생 작업을 처리하는 PlaybackManager를 만듭니다. 다른 구성은 필요하지 않습니다.
seo-description: HLS 스트림 설정 및 재생 작업을 처리하는 PlaybackManager를 만듭니다. 다른 구성은 필요하지 않습니다.
seo-title: 비디오 재생 활성화
title: 비디오 재생 활성화
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# 비디오 재생 활성화 {#enable-video-playback}

HLS 스트림 설정 및 재생 작업을 처리하는 PlaybackManager를 만듭니다. 다른 구성은 필요하지 않습니다.

1. 다음 코드가 에 있는지 확인하여 미디어 플레이어 개체를 만듭니다 [!DNL PlayerFragment.java].

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. 다음을 통해 재생 관리자를 `ManagerFactory`만듭니다.

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 재생 `PlaybackManagerEventListener` 이벤트를 `PlayerFragment` 처리하도록 에서 를 구현합니다.

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. 이벤트 리스너를 `PlayerFragment`다음과 같이 등록합니다.

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 비디오 리소스를 설정합니다.

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. 다음 위치에서 제어 막대 작업을 `PlayerFragment`설정합니다.

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 관련 API 설명서 {#related-api-documentation}

* [Class PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)