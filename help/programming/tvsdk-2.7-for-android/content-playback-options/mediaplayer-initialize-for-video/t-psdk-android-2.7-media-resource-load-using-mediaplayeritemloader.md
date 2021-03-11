---
description: MediaPlayerItemLoader를 사용하면 MediaPlayer 인스턴스를 인스턴스화하지 않고도 미디어 스트림에 대한 정보를 얻을 수 있습니다. 이 기능은 버퍼링 전 스트림에서 특히 유용하므로 재생 시간이 지연되지 않고 바로 시작될 수 있습니다.
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}을(를) 사용하여 미디어 리소스 로드

MediaPlayerItemLoader를 사용하면 MediaPlayer 인스턴스를 인스턴스화하지 않고도 미디어 스트림에 대한 정보를 얻을 수 있습니다. 이 기능은 버퍼링 전 스트림에서 특히 유용하므로 재생 시간이 지연되지 않고 바로 시작될 수 있습니다.

`MediaPlayerItemLoader` 클래스는 비디오 디코딩 하드웨어 리소스를 할당하는 `MediaPlayer` 인스턴스에 보기를 첨부하지 않고 현재 `MediaPlayerItem`에 대한 미디어 리소스를 교환하는 데 도움이 됩니다. DRM으로 보호된 콘텐츠에 추가 단계가 필요하지만 이 설명서에서는 이 단계를 설명하지 않습니다.

>[!IMPORTANT]
>
>TVSDK는 `itemLoader` 및 `MediaPlayer` 모두에서 작동하는 단일 `QoSProvider`을(를) 지원하지 않습니다. 응용 프로그램에서 Instant On을 사용하는 경우 응용 프로그램은 2개의 `QoS` 인스턴스를 유지 관리하고 이 정보에 대해 두 인스턴스를 모두 관리해야 합니다. 자세한 내용은 [instant-on](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md)을 참조하십시오.

1. `MediaPlayerItemLoader` 인스턴스를 만듭니다.

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
   >각 리소스에 대해 별도의 `MediaPlayerItemLoader` 인스턴스를 만듭니다. 하나의 `MediaPlayerItemLoader` 인스턴스를 사용하여 여러 리소스를 로드하지 마십시오.

1. `MediaPlayerItemLoader` 인스턴스에서 알림을 수신하도록 `ItemLoaderListener` 클래스를 구현합니다.

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

   `onLoadComplete()` 콜백에서 다음 중 하나를 수행합니다.

   * 버퍼링에 영향을 줄 수 있는 것(예: WebVTT 또는 오디오 트랙 선택)이 완료되었는지 확인하고 `prepareBuffer()`을(를) 호출하여 즉시 사용할 수 있습니다.
   * `replaceCurrentItem()`을 사용하여 `MediaPlayer` 인스턴스에 항목을 첨부합니다.

   `prepareBuffer()`을(를) 호출하면 준비가 완료되면 `onBufferPrepared` 핸들러에서 BUFFER_PREPARED 이벤트를 받게 됩니다.

1. `MediaPlayerItemLoader` 인스턴스에서 `load`을 호출하고 로드할 리소스와 선택적으로 내용 ID 및 `MediaPlayerItemConfig` 인스턴스를 전달합니다.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 스트림의 시작 부분이 아닌 지점에서 버퍼링하려면 버퍼링을 시작할 위치(밀리초)를 사용하여 `prepareBuffer()`을(를) 호출합니다.
1. `MediaPlayer`의 `replaceCurrentItem()` 및 `play()` 메서드를 사용하여 해당 지점에서 재생을 시작합니다.
1. 유휴 상태를 기다린 후 `replaceCurrentItem`으로 전화하십시오.
1. 항목을 재생합니다.

   * 항목이 로드되었지만 버퍼링되지 않은 경우:

      1. 초기화된 상태를 기다립니다.
      1. `prepareToPlay()`을(를) 호출합니다.
      1. 준비 상태를 기다립니다.
      1. `play()`을(를) 호출합니다.
   * 항목이 버퍼링되는 경우:

      1. 버퍼 준비 이벤트를 기다립니다.
      1. `play()`을(를) 호출합니다.