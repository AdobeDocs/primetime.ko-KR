---
description: 즉시 활성화하면 하나 이상의 채널이 미리 로드됩니다. 사용자가 채널을 선택하거나 채널을 전환하면 컨텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.
seo-description: 즉시 활성화하면 하나 이상의 채널이 미리 로드됩니다. 사용자가 채널을 선택하거나 채널을 전환하면 컨텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.
seo-title: 즉시 켜기
title: 즉시 켜기
uuid: 7e14b779-2a36-4ff4-a365-9ac49a836ff3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# 즉시 켜기 {#instant-on}

즉시 활성화하면 하나 이상의 채널이 미리 로드됩니다. 사용자가 채널을 선택하거나 채널을 전환하면 컨텐츠가 즉시 재생됩니다. 버퍼링은 사용자가 시청을 시작할 때까지 완료됩니다.

Instant On 없이 TVSDK는 재생할 미디어를 초기화하지만 응용 프로그램이 호출될 때까지 스트림을 버퍼링하지 않습니다 `play`. 버퍼링이 완료될 때까지 사용자에게 컨텐츠가 표시되지 않습니다. Instant On을 사용하면 여러 미디어 플레이어(또는 미디어 플레이어 항목 로더) 인스턴스를 실행할 수 있으며 TVSDK가 스트림을 즉시 버퍼링하기 시작합니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 `play` 호출하면 즉시 재생이 시작됩니다.

TVSDK를 실행할 수 있는 인스턴스 수와 인스턴스 수에 제한이 없지만 더 많은 인스턴스를 실행하면 더 많은 리소스가 소모됩니다. `MediaPlayer` `MediaPlayerItemLoader` 실행 중인 인스턴스 수의 애플리케이션 성능에 영향을 줄 수 있습니다. 자세한 `MediaPlayerItemLoader`내용은 미디어 플레이어에서 [미디어 리소스 로드를 참조하십시오](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK는 단일 TV `QoSProvider` 를 `itemLoader` 및 `MediaPlayer`두 가지 모두와 함께 사용할 수 없습니다. 고객이 Instant On을 사용하는 경우 애플리케이션은 두 개의 QoS 인스턴스를 유지하고 두 인스턴스를 모두 관리하여 정보를 관리해야 합니다.

자세한 내용은 `MediaPlayerItemLoader`MediaPlayerItemLoader [를 사용하여 미디어 리소스 로드를 참조하십시오](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

## mediaPlayerItemLoader에 QoS 공급자 인스턴스 추가 {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* QoS 공급자 생성 및 `mediaPlayerItemLoader` 인스턴스에 첨부

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   재생이 시작되면 QoSdata `_qosProvider` 를 사용하여 데이터를 `timeToLoad` 얻고 `timeToPrepare` 저장할 수 있습니다. 나머지 QoS 지표는 에 `QoSProvider` 첨부된 를 사용하여 검색할 수 `mediaPlayer`있습니다.

   자세한 내용은 `MediaPlayerItemLoader`MediaPlayerItemLoader [를 사용하여 미디어 리소스 로드를 참조하십시오](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader).

## 즉시 켜기 위해 버퍼링 구성 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK는 미디어 리소스와 함께 즉시 켜기를 사용할 수 있는 방법과 상태를 제공합니다.

>[!NOTE]
>
>Adobe는 InstantOn `MediaPlayerItemLoader` 에 사용할 것을 권장합니다. 대신 `MediaPlayerItemLoader``MediaPlayer`사용하려면 media-resource-load-using-mediaplayertiemloader를 참조하십시오.

1. 리소스가 로드되었고 플레이어가 리소스를 재생할 준비가 되었는지 확인합니다.
1. 호출하기 `play`전에 각 `prepareBuffer` `MediaPlayer` 인스턴스를 호출하십시오.

   >[!NOTE]
   >
   >`prepareBuffer` instant On을 활성화하면 TVSDK가 즉시 버퍼링을 시작하고 버퍼가 가득 차면 이벤트를 `BUFFERING_COMPLETED` 전달합니다.

   >[!TIP]
   >
   >기본적으로 미디어 스트림을 `prepareBuffer` 설정하고 `prepareToPlay` 처음부터 재생을 시작하도록 설정합니다. 다른 위치에서 시작하려면 위치(밀리초)를 `prepareToPlay`로 전달합니다.

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

1. 이벤트를 받으면 항목 재생을 시작하거나 컨텐츠가 완전히 버퍼링되었음을 나타내는 시각적 피드백을 표시합니다. `BUFFERING_COMPLETE`

   >[!NOTE]
   >
   >전화한 `play`경우 재생을 즉시 시작해야 합니다.

