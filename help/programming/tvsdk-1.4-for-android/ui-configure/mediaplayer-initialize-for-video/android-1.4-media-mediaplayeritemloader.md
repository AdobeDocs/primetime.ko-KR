---
description: 미디어 리소스를 확인하는 또 다른 방법은 MediaPlayerItemLoader를 사용하는 것입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻고자 할 때 유용합니다.
title: MediaPlayerItemLoader를 사용하여 미디어 리소스 로드
exl-id: 9d129497-8a71-433a-a542-f49be519893b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# MediaPlayerItemLoader를 사용하여 미디어 리소스 로드 {#load-a-media-resource-using-mediaplayeritemloader}

미디어 리소스를 확인하는 또 다른 방법은 MediaPlayerItemLoader를 사용하는 것입니다. 이 기능은 MediaPlayer 인스턴스를 인스턴스화하지 않고 특정 미디어 스트림에 대한 정보를 얻고자 할 때 유용합니다.

다음을 통해 `MediaPlayerItemLoader` 클래스에서 해당 미디어 리소스와 교환할 수 있습니다. `MediaPlayerItem` 에 보기를 첨부하지 않고 `MediaPlayer` 비디오 디코딩 하드웨어 리소스의 할당을 초래하는 인스턴스. 을(를) 가져오는 프로세스 `MediaPlayerItem` 인스턴스가 비동기적입니다.

1. 구현 `MediaPlayerItemLoader.LoaderListener` 콜백 인터페이스입니다.

       이 인터페이스는 다음 두 가지 방법을 정의합니다.
   
   * `LoaderListener.onError` callback 함수

      TVSDK는 이 함수를 사용하여 오류가 발생했음을 애플리케이션에 알립니다. TVSDK는 오류 코드를 매개 변수로 제공하고 진단 정보가 포함된 설명 문자열을 제공합니다.

   * `LoaderListener.onError` callback 함수

      TVSDK는 이 함수를 사용하여 요청된 정보를 의 형식으로 사용할 수 있음을 애플리케이션에 알립니다. `MediaPlayerItem` 콜백에 매개 변수로 전달되는 인스턴스입니다.

1. 이 인스턴스를 TVSDK의 생성자에 매개 변수로 전달하여 TVSDK에 등록합니다. `MediaPlayerItemLoader`.
1. 호출 `MediaPlayerItemLoader.load`, 인스턴스 전달 `MediaResource` 개체.

   의 URL `MediaResource` 개체는 정보를 가져올 스트림을 가리켜야 합니다. 예:

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
