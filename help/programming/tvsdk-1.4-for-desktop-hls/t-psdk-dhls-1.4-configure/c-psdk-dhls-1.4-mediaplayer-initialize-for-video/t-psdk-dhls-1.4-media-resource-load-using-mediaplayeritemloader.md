---
description: 미디어 리소스를 확인하는 또 다른 방법은 MediaPlayerItemLoader를 사용하는 것입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻고자 할 때 유용합니다.
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# MediaPlayerItemLoader를 사용하여 미디어 리소스 로드{#load-a-media-resource-using-mediaplayeritemloader}

미디어 리소스를 확인하는 또 다른 방법은 MediaPlayerItemLoader를 사용하는 것입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻고자 할 때 유용합니다.

다음을 통해 `MediaPlayerItemLoader` 클래스에서 해당 미디어 리소스와 교환할 수 있습니다. `MediaPlayerItem` 에 보기를 첨부하지 않고 `MediaPlayer` 비디오 디코딩 하드웨어 리소스의 할당을 초래하는 인스턴스. 을(를) 가져오는 프로세스 `MediaPlayerItem` 인스턴스가 비동기적입니다.

1. 이에 대한 이벤트 리스너 구현 `MediaPlayerItemLoader` 이벤트:

   * `MediaPlayerItemLoaderEvent.ERROR` 이벤트

     TVSDK는 이 함수를 사용하여 오류가 발생했음을 애플리케이션에 알립니다. TVSDK는 진단 정보가 포함된 오류 속성을 제공합니다.

1. 이 인스턴스를 다음에 등록 `MediaPlayerItemLoader`.
1. 호출 `DefaultMediaPlayerItemLoader.load`, 인스턴스 전달 `MediaResource` 개체.

   의 URL `MediaResource` 개체는 정보를 가져올 스트림을 가리켜야 합니다. 예:

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
