---
description: 미디어 리소스를 해결하는 또 다른 방법은 MediaPlayerItemLoader입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻고자 할 때 유용합니다.
seo-description: 미디어 리소스를 해결하는 또 다른 방법은 MediaPlayerItemLoader입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻고자 할 때 유용합니다.
seo-title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}을(를) 사용하여 미디어 리소스 로드

미디어 리소스를 해결하는 또 다른 방법은 MediaPlayerItemLoader입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻고자 할 때 유용합니다.

`MediaPlayerItemLoader` 클래스를 통해, 보기를 `MediaPlayer` 인스턴스에 첨부하지 않고 해당 `MediaPlayerItem`에 대한 미디어 리소스를 교환할 수 있으므로 비디오 디코딩 하드웨어 리소스가 할당됩니다. `MediaPlayerItem` 인스턴스를 가져오는 프로세스는 비동기적입니다.

1. `MediaPlayerItemLoader.LoaderListener` 콜백 인터페이스를 구현합니다.

       이 인터페이스는 다음 두 가지 방법을 정의합니다.
   
   * `LoaderListener.onError` 콜백 함수

      TVSDK에서는 이 방법을 사용하여 오류가 발생했음을 애플리케이션에 알립니다. TVSDK는 오류 코드를 매개 변수로 제공하고 진단 정보가 포함된 설명 문자열을 제공합니다.

   * `LoaderListener.onError` 콜백 함수

      TVSDK는 이 방법을 사용하여 요청된 정보를 콜백으로 매개 변수로 전달되는 `MediaPlayerItem` 인스턴스의 형태로 사용할 수 있음을 응용 프로그램에 알립니다.

1. 이 인스턴스를 `MediaPlayerItemLoader` 생성자에 매개 변수로 전달하여 TVSDK에 등록합니다.
1. `MediaPlayerItemLoader.load`을(를) 호출하여 `MediaResource` 개체의 인스턴스를 전달합니다.

   `MediaResource` 개체의 URL은 정보를 얻을 스트림을 가리켜야 합니다. 예:

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

