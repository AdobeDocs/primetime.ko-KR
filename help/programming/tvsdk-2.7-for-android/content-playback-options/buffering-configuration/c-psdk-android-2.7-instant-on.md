---
description: 즉시 활성화하면 하나 이상의 채널이 미리 로드됩니다. 사용자가 채널을 선택하거나 채널을 전환할 때 컨텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.
seo-description: 즉시 활성화하면 하나 이상의 채널이 미리 로드됩니다. 사용자가 채널을 선택하거나 채널을 전환할 때 컨텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.
seo-title: 즉시 켜기
title: 즉시 켜기
uuid: 7e14b779-2a36-4ff4-a365-9ac49a836ff3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# {#instant-on}에 인스턴트

즉시 활성화하면 하나 이상의 채널이 미리 로드됩니다. 사용자가 채널을 선택하거나 채널을 전환할 때 컨텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.

TVSDK가 인스턴트 켜기 없이 재생될 미디어를 초기화하지만 응용 프로그램이 `play`을 호출하기 전까지 스트림을 버퍼링하지 않습니다. 버퍼링이 완료될 때까지 사용자에게 컨텐츠가 표시되지 않습니다. Instant On을 사용하면 여러 미디어 플레이어(또는 미디어 플레이어 항목 로더) 인스턴스를 실행할 수 있으며 TVSDK가 스트림을 즉시 버퍼링하기 시작합니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 `play`을(를) 호출하면 즉시 재생이 시작됩니다.

TVSDK가 실행할 수 있는 `MediaPlayer` 및 `MediaPlayerItemLoader` 인스턴스의 수에 제한이 없지만 더 많은 인스턴스를 실행하면 더 많은 리소스가 소모됩니다. 실행 중인 인스턴스 수의 애플리케이션 성능에 영향을 줄 수 있습니다. `MediaPlayerItemLoader`에 대한 자세한 내용은 미디어 플레이어](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md)에서 미디어 리소스 로드를 참조하십시오.[

>[!IMPORTANT]
>
>TVSDK는 `itemLoader` 및 `MediaPlayer` 모두에서 작동하는 단일 `QoSProvider`을 지원하지 않습니다. 고객이 Instant On을 사용하는 경우 애플리케이션은 두 개의 QoS 인스턴스를 유지하고 정보를 위해 두 인스턴스를 모두 관리해야 합니다.

`MediaPlayerItemLoader`에 대한 자세한 내용은 [MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)를 사용하여 미디어 리소스 로드를 참조하십시오.

## mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}에 QoS 공급자 인스턴스 추가

* QoS 공급자를 만들어 `mediaPlayerItemLoader` 인스턴스에 첨부

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   재생이 시작되면 `_qosProvider`을(를) 사용하여 `timeToLoad` 및 `timeToPrepare` QoSdata를 가져옵니다. 나머지 QoS 지표는 `mediaPlayer`에 첨부된 `QoSProvider`을 사용하여 검색할 수 있습니다.

   `MediaPlayerItemLoader`에 대한 자세한 내용은 [MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader)를 사용하여 미디어 리소스 로드를 참조하십시오.

## {#section_4FE346B7BE434BA8A2203896D6E52146}에 즉시 버퍼링을 구성합니다.

TVSDK는 미디어 리소스와 함께 즉시 켜기를 사용할 수 있는 방법과 상태를 제공합니다.

>[!NOTE]
>
>Adobe은 InstantOn에 `MediaPlayerItemLoader`을 사용하는 것이 좋습니다. `MediaPlayer` 대신 `MediaPlayerItemLoader`을 사용하려면 media-resource-load-using-mediaplayertiemloader를 참조하십시오.

1. 리소스가 로드되었고 플레이어가 리소스를 재생할 준비가 되었는지 확인합니다.
1. `play`을(를) 호출하기 전에 각 `MediaPlayer` 인스턴스에 대해 `prepareBuffer`을(를) 호출합니다.

   >[!NOTE]
   >
   >`prepareBuffer` [인스턴트 온]을 활성화하면 TVSDK가 즉시 버퍼링을 시작하고 버퍼가 가득 차면  `BUFFERING_COMPLETED` 이벤트를 전달합니다.

   >[!TIP]
   >
   >기본적으로 `prepareBuffer` 및 `prepareToPlay`은 미디어 스트림을 설정하여 처음부터 재생을 시작합니다. 다른 위치에서 시작하려면 위치(밀리초)를 `prepareToPlay`으로 전달합니다.

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. `BUFFERING_COMPLETE` 이벤트를 받으면 항목 재생을 시작하거나 컨텐츠가 완전히 버퍼링되었음을 나타내는 시각적 피드백을 표시합니다.

   >[!NOTE]
   >
   >`play`을(를) 호출하는 경우 재생을 즉시 시작해야 합니다.

