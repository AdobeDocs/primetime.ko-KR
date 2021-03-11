---
description: 미디어 리소스를 해결하는 또 다른 방법은 MediaPlayerItemLoader입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻을 때 유용합니다.
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}을(를) 사용하여 미디어 리소스 로드

미디어 리소스를 해결하는 또 다른 방법은 MediaPlayerItemLoader입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻을 때 유용합니다.

`MediaPlayerItemLoader` 클래스를 통해 `MediaPlayer` 인스턴스에 보기를 첨부하지 않고 해당 `MediaPlayerItem`에 대한 미디어 리소스를 교환할 수 있으므로 비디오 디코딩 하드웨어 리소스가 할당될 수 있습니다. `MediaPlayerItem` 인스턴스를 가져오는 프로세스는 비동기적입니다.

1. `MediaPlayerItemLoader.LoaderListener` 콜백 인터페이스를 구현합니다.

       이 인터페이스는 다음 두 가지 방법을 정의합니다.
   
   * `LoaderListener.onError` 콜백 함수

      TVSDK에서는 이 옵션을 사용하여 오류가 발생했음을 애플리케이션에 알립니다. TVSDK는 오류 코드를 매개 변수로 제공하고 진단 정보가 포함된 설명 문자열을 제공합니다.

   * `LoaderListener.onError` 콜백 함수

      TVSDK는 이 정보를 사용하여 요청된 정보를 콜백으로 매개 변수로 전달되는 `MediaPlayerItem` 인스턴스의 형태로 응용 프로그램에 알려줍니다.

1. 이 인스턴스를 `MediaPlayerItemLoader` 생성자에 매개 변수로 전달하여 TVSDK에 등록합니다.
1. `MediaResource` 객체의 인스턴스를 전달하는 `MediaPlayerItemLoader.load`을(를) 호출합니다.

   `MediaResource` 개체의 URL은 정보를 가져올 스트림을 가리켜야 합니다. 예:

   ```java
   // instantiate the listener interface 
   MediaPlayerItemLoader.LoaderListener _itemLoaderListener = 
     new MediaPlayerItemLoader.LoaderListener() { 
       @Override 
       public void onError(MediaErrorCode mediaErrorCode, String description) { 
           // something went wrong - look at the error code and description 
       } 
       @Override 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
           // information is available - look at the data in the "playerItem" object 
       } 
   } 
   
   // instantiate the MediaPlayerItemLoader object (pass the listener as parameter) 
   MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(_itemLoaderListener); 
   
   // create the MediaResource instance and set the URL to point to the actual media stream 
   MediaResource mediaResource =  
     MediaResource.createFromUrl("https://test.com/test_media.m3u8", null); 
   
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

