---
description: MediaPlayerItemLoader를 사용하면 MediaPlayer 인스턴스를 인스턴스화하지 않고도 미디어 스트림에 대한 정보를 얻을 수 있습니다. 이 기능은 재생 속도를 지연시키지 않고 시작할 수 있도록 미리 버퍼링 스트림에서 특히 유용합니다.
seo-description: MediaPlayerItemLoader를 사용하면 MediaPlayer 인스턴스를 인스턴스화하지 않고도 미디어 스트림에 대한 정보를 얻을 수 있습니다. 이 기능은 재생 속도를 지연시키지 않고 시작할 수 있도록 미리 버퍼링 스트림에서 특히 유용합니다.
seo-title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
uuid: 504063af-1dd4-4268-88e7-ad5a247fdff7
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# MediaPlayerItemLoader를 사용하여 미디어 리소스 로드 {#load-a-media-resource-using-mediaplayeritemloader}

MediaPlayerItemLoader를 사용하면 MediaPlayer 인스턴스를 인스턴스화하지 않고도 미디어 스트림에 대한 정보를 얻을 수 있습니다. 이 기능은 재생 속도를 지연시키지 않고 시작할 수 있도록 미리 버퍼링 스트림에서 특히 유용합니다.

이 `MediaPlayerItemLoader` 클래스는 뷰를 인스턴스에 연결하지 `MediaPlayerItem` `MediaPlayer` 않고 현재 미디어 리소스를 교환하는 데 도움이 되며, 이렇게 하면 비디오 디코딩 하드웨어 리소스가 할당됩니다. DRM으로 보호된 콘텐츠에 대한 추가 단계는 필요하지만 이 설명서에는 이러한 단계가 설명되어 있지 않습니다.

>[!IMPORTANT]
>
>TVSDK는 단일 TV `QoSProvider` 를 `itemLoader` 및 `MediaPlayer`두 가지 모두와 함께 사용할 수 없습니다. 응용 프로그램에서 인스턴트 온을 사용하는 경우 응용 프로그램은 두 개의 `QoS` 인스턴스를 유지하고 두 인스턴스를 모두 관리해야 합니다. 자세한 [내용은 Instant-on](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) 을 참조하십시오.

1. 인스턴스를 `MediaPlayerItemLoader`만듭니다.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
   
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
   
           public void onBufferingBegin() { 
               //Do something 
           } 
   
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   ```

   >[!TIP]
   >
   >각 리소스에 대해 별도의 인스턴스를 `MediaPlayerItemLoader` 만듭니다. 하나의 `MediaPlayerItemLoader` 인스턴스를 사용하여 여러 리소스를 로드하지 마십시오.

1. 인스턴스로부터 알림을 수신할 `ItemLoaderListener` 클래스를 구현합니다 `MediaPlayerItemLoader` .

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   콜백에서 `onLoadComplete()` 다음 중 하나를 수행합니다.

   * WebVTT 또는 오디오 트랙을 선택하는 등 버퍼링에 영향을 줄 수 있는 모든 것이 완료되어 즉각적인 `prepareBuffer()` 사용을 위해 호출되는지 확인합니다.
   * 를 사용하여 항목을 `MediaPlayer` 인스턴스에 첨부합니다 `replaceCurrentItem()`.
   호출을 `prepareBuffer()`하면 준비가 완료되면 처리기에서 BUFFER_PREPARED 이벤트를 `onBufferPrepared` 받게 됩니다.
1. 인스턴스를 `load` 호출하고 로드할 리소스와 선택적으로 컨텐츠 ID 및 `MediaPlayerItemLoader` `MediaPlayerItemConfig` 인스턴스를 전달합니다.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 스트림 시작 이외의 지점에서 버퍼링하려면 버퍼링을 시작할 위치(밀리초) `prepareBuffer()` 를 사용하여 호출합니다.
1. 이 시점에서 재생을 `replaceCurrentItem()` 시작하려면 및 `play()` `MediaPlayer` 메서드를 사용합니다.
1. 유휴 상태를 기다렸다가 `replaceCurrentItem`호출합니다.
1. 항목을 재생합니다.

   * 항목이 로드되었지만 버퍼링되지 않은 경우:

      1. 초기화된 상태를 기다립니다.
      1. 전화 `prepareToPlay()`걸기
      1. 준비된 상태 대기
      1. 전화 `play()`걸기
   * 항목이 버퍼링되는 경우:

      1. 버퍼 준비 이벤트를 기다립니다.
      1. 전화 `play()`걸기