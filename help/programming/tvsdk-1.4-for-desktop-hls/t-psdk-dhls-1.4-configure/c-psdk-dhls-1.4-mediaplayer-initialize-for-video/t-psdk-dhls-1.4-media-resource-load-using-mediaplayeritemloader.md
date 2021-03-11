---
description: 미디어 리소스를 해결하는 또 다른 방법은 MediaPlayerItemLoader입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻을 때 유용합니다.
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}를 사용하여 미디어 리소스 로드

미디어 리소스를 해결하는 또 다른 방법은 MediaPlayerItemLoader입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻을 때 유용합니다.

`MediaPlayerItemLoader` 클래스를 통해 `MediaPlayer` 인스턴스에 보기를 첨부하지 않고 해당 `MediaPlayerItem`에 대한 미디어 리소스를 교환할 수 있으므로 비디오 디코딩 하드웨어 리소스가 할당될 수 있습니다. `MediaPlayerItem` 인스턴스를 가져오는 프로세스는 비동기적입니다.

1. 이러한 `MediaPlayerItemLoader` 이벤트에 대한 이벤트 리스너를 구현합니다.

   * `MediaPlayerItemLoaderEvent.ERROR` event

      TVSDK에서는 이 옵션을 사용하여 오류가 발생했음을 애플리케이션에 알립니다. TVSDK는 진단 정보가 포함된 오류 속성을 제공합니다.

1. 이 인스턴스를 `MediaPlayerItemLoader`에 등록합니다.
1. `MediaResource` 객체의 인스턴스를 전달하는 `DefaultMediaPlayerItemLoader.load`을(를) 호출합니다.

   `MediaResource` 개체의 URL은 정보를 가져올 스트림을 가리켜야 합니다. 예:

   ```
   private function onLoadError(event:MediaPlayerItemLoaderEvent):void { 
       // something went wrong - look at the error code and description 
       // contained within the event.error 
   } 
   private function onLoadCompleted(event:MediaPlayerItemLoaderEvent):void { 
       // information is available - look at the data in the "event.item" object 
   } 
   // instantiate the MediaPlayerItemLoader object and register event listeners 
   var itemLoader:MediaPlayerItemLoader = new DefaultMediaPlayerItemLoader(); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.ERROR, onLoadError); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.COMPLETED, onLoadCompleted); 
   // create the MediaResource instance and set the URL to point to the actual media stream 
   var mediaResource:MediaResource = 
     MediaResource.createFromURL("https://example.com/media/test_media.m3u8", null); 
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

