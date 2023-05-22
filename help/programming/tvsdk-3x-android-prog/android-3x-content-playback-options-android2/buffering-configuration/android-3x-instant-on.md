---
description: 에서 즉시 활성화란 하나 이상의 채널이 미리 로드됨을 의미합니다. 사용자가 채널을 선택하거나 채널을 전환하면 콘텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.
title: 즉시 사용
exl-id: 59293e07-160a-41a2-8ffe-7ca9323048f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 즉시 사용 {#instant-on}

에서 즉시 활성화란 하나 이상의 채널이 미리 로드됨을 의미합니다. 사용자가 채널을 선택하거나 채널을 전환하면 콘텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.

인스턴트 온 없이 TVSDK는 재생할 미디어를 초기화하지만 애플리케이션이 호출될 때까지 스트림 버퍼링을 시작하지 않습니다 `play`. 버퍼링이 완료될 때까지 콘텐츠가 표시되지 않습니다. Instant On을 사용하면 여러 미디어 플레이어(또는 미디어 플레이어 항목 로더) 인스턴스를 시작할 수 있으며 TVSDK가 즉시 스트림 버퍼링을 시작합니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 호출 `play` 새 채널에서 즉시 재생을 시작합니다.

의 수에는 제한이 없지만 `MediaPlayer` 및 `MediaPlayerItemLoader` tvsdk가 실행할 수 있는 인스턴스는 더 많은 인스턴스를 실행하므로 더 많은 리소스를 사용합니다. 실행 중인 인스턴스 수에 따라 응용 프로그램 성능이 영향을 받을 수 있습니다. 에 대한 자세한 내용 `MediaPlayerItemLoader`, 참조 [미디어 플레이어에서 미디어 리소스 로드](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK는 단일 `QoSProvider` 두 가지 모두를 사용하여 작업 `itemLoader` 및 `MediaPlayer`. 고객이 Instant On을 사용하는 경우 애플리케이션은 두 개의 QoS 인스턴스를 유지 관리하고 두 인스턴스를 모두 관리하여 정보를 관리해야 합니다.

에 대한 자세한 내용 `MediaPlayerItemLoader`, 참조 [MediaPlayerItemLoader를 사용하여 미디어 리소스 로드](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## mediaPlayerItemLoader에 QoS 공급자 인스턴스 추가 {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* QoS 공급자 만들기 및 연결 `mediaPlayerItemLoader` 인스턴스

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   재생이 시작되면 를 사용합니다. `_qosProvider` 다운로드하려면 `timeToLoad` 및 `timeToPrepare` QoSdata. 나머지 QoS 지표는 `QoSProvider` 이(가) 다음에 첨부되었습니다. `mediaPlayer`.

   에 대한 자세한 내용 `MediaPlayerItemLoader`, 참조 [MediaPlayerItemLoader를 사용하여 미디어 리소스 로드](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## 즉시 사용할 수 있도록 버퍼링 구성 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK는 미디어 리소스와 함께 Instant On을 사용할 수 있는 메서드와 상태를 제공합니다.

>[!NOTE]
>
>Adobe은 다음을 권장합니다. `MediaPlayerItemLoader` 인스턴트 온용. 사용 `MediaPlayerItemLoader`, 대신 `MediaPlayer`, 참조 [MediaPlayerItemLoader를 사용하여 미디어 리소스 로드](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. 리소스가 로드되었는지, 플레이어가 리소스를 재생할 준비가 되었는지 확인합니다.
1. 호출 전 `play`, 호출 `prepareBuffer` 각 `MediaPlayer` 인스턴스.

   `prepareBuffer` instant On을 활성화하면 TVSDK가 즉시 버퍼링을 시작하고 를 디스패치합니다. `BUFFERING_COMPLETED` 버퍼가 가득 찬 경우의 이벤트입니다.

   >[!TIP]
   >
   >기본적으로, `prepareBuffer` 및 `prepareToPlay` 미디어 스트림을 설정하여 처음부터 재생을 시작합니다. 다른 위치에서 시작하려면 해당 위치(밀리초)를에 전달합니다. `prepareToPlay`.

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

1. 다음을 받을 때 `BUFFERING_COMPLETE` 이벤트가 발생하면 항목 재생을 시작하거나 콘텐츠가 완전히 버퍼링되었음을 나타내는 시각적 피드백을 표시합니다.

   >[!NOTE]
   >
   >전화 주시면 `play`, 재생이 즉시 시작됩니다.
