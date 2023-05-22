---
description: HLS 스트림 설정 및 재생 작업을 처리하는 PlaybackManager 를 만듭니다. 다른 구성은 필요하지 않습니다.
title: 비디오 재생 활성화
exl-id: b53f602b-5752-4471-9905-2e4351dfc8d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 비디오 재생 활성화 {#enable-video-playback}

HLS 스트림 설정 및 재생 작업을 처리하는 PlaybackManager 를 만듭니다. 다른 구성은 필요하지 않습니다.

1. 다음 코드가에 있는지 확인하여 미디어 플레이어 개체 만들기 [!DNL PlayerFragment.java]:

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. 다음을 통해 재생 관리자 만들기 `ManagerFactory`:

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. 구현 `PlaybackManagerEventListener` 다음에서 `PlayerFragment` 재생 이벤트를 처리하려면 다음을 수행하십시오.

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. 에서 이벤트 리스너 등록 `PlayerFragment`:

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. 비디오 리소스를 설정합니다.

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. 에서 컨트롤 막대 작업을 설정합니다. `PlayerFragment`:

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## 관련 API 설명서 {#related-api-documentation}

* [클래스 PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListen](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)
