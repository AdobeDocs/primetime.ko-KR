---
description: MediaPlayerItemLoader를 사용하면 MediaPlayer 인스턴스를 인스턴스화하지 않고도 미디어 스트림에 대한 정보를 얻을 수 있습니다. 이 기능은 지연 없이 재생을 시작할 수 있도록 스트림을 미리 버퍼링하는 데 특히 유용합니다.
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
exl-id: 6bd081bb-b92b-4c0a-a3bc-ef2128d0d8bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# MediaPlayerItemLoader를 사용하여 미디어 리소스 로드 {#load-a-media-resource-using-mediaplayeritemloader}

MediaPlayerItemLoader를 사용하면 MediaPlayer 인스턴스를 인스턴스화하지 않고도 미디어 스트림에 대한 정보를 얻을 수 있습니다. 이 기능은 지연 없이 재생을 시작할 수 있도록 스트림을 미리 버퍼링하는 데 특히 유용합니다.

다음 `MediaPlayerItemLoader` 클래스는 현재 미디어 리소스를 교환하는 데 도움이 됩니다. `MediaPlayerItem` 에 보기를 첨부하지 않고 `MediaPlayer` 비디오 디코딩 하드웨어 리소스를 할당하는 인스턴스. DRM으로 보호된 콘텐츠에는 추가 단계가 필요하지만 이 설명서에서는 이를 설명하지 않습니다.

>[!IMPORTANT]
>
>TVSDK는 단일 `QoSProvider` 두 가지 모두를 사용하여 작업 `itemLoader` 및 `MediaPlayer`. 응용 프로그램에서 Instant On을 사용하는 경우 응용 프로그램에서 두 가지를 유지 관리해야 합니다 `QoS` 인스턴스 및 두 인스턴스 모두를 관리하여 정보를 제공합니다. 다음을 참조하십시오  [인스턴트 온](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) 추가 정보.

1. 의 인스턴스 만들기 `MediaPlayerItemLoader`.

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
   >의 별도 인스턴스 만들기 `MediaPlayerItemLoader` 각 리소스에 대해 사용하지 않음 `MediaPlayerItemLoader` 여러 리소스를 로드할 인스턴스입니다.

1. 구현 `ItemLoaderListener` 에서 알림을 받을 클래스 `MediaPlayerItemLoader` 인스턴스.

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

   다음에서 `onLoadComplete()` callback, 다음 중 하나를 수행합니다.

   * 버퍼링에 영향을 줄 수 있는 모든 항목(예: WebVTT 또는 오디오 트랙 선택)이 완료되었는지 확인하고 호출합니다 `prepareBuffer()` 인스턴트 아티클을 활용하기 위해.
   * 항목을 다음에 첨부 `MediaPlayer` 를 사용한 인스턴스 `replaceCurrentItem()`.
   전화 주시면 `prepareBuffer()`에서는 BUFFER_PREPARED 이벤트를 받습니다. `onBufferPrepared` 준비가 완료되면 처리기를 실행합니다.

1. 호출 `load` 다음에 있음 `MediaPlayerItemLoader` 을(를) 인스턴스화하고 로드할 리소스, 선택적으로 콘텐츠 ID 및 `MediaPlayerItemConfig` 인스턴스.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 스트림의 시작 지점이 아닌 다른 지점에서 버퍼링하려면 를 호출합니다. `prepareBuffer()` 버퍼링을 시작할 위치(밀리초)입니다.
1. 사용 `replaceCurrentItem()` 및 `play()` 방법 `MediaPlayer` 해당 시점부터 재생을 시작합니다.
1. 유휴 상태 대기 및 호출 `replaceCurrentItem`.
1. 항목을 재생합니다.

   * 항목이 로드되었지만 버퍼링되지 않은 경우:

      1. 초기화된 상태 대기.
      1. 호출 `prepareToPlay()`.
      1. PREPARED 상태를 기다립니다.
      1. 호출 `play()`.
   * 항목이 버퍼링되는 경우:

      1. 버퍼 준비 이벤트를 기다립니다.
      1. 호출 `play()`.
