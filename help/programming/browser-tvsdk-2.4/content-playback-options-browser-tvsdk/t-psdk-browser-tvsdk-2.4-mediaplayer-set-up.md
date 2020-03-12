---
description: MediaPlayer 개체는 미디어 플레이어의 비헤이비어와 기능을 캡슐화합니다.
seo-description: MediaPlayer 개체는 미디어 플레이어의 비헤이비어와 기능을 캡슐화합니다.
seo-title: MediaPlayer 설정
title: MediaPlayer 설정
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc

---


# MediaPlayer 설정{#set-up-the-mediaplayer}

MediaPlayer 개체는 미디어 플레이어의 비헤이비어와 기능을 캡슐화합니다.

1. 다음을 사용하여 `MediaPlayer` 인스턴스화합니다.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 인스턴스 `MediaPlayerView` 만들기:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   여기서 `container` 는 를 포함하는 대상 `div` 요소입니다 `HTMLMediaElement`.

   예를 들어 HTML 페이지에서 다음을 수행합니다.

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   전화 문의:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. 인스턴스에 `MediaPlayerView` `MediaPlayer` 인스턴스 첨부:

   ```js
   player.view = view;
   ```

1. 사용자 정의 컨트롤 `div` 요소를 MediaPlayer 인스턴스에 연결합니다.

   예를 들어, HTML에서는

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   전화 문의:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

이제 `MediaPlayer` 인스턴스를 사용할 수 있으며 장치 화면에 비디오 컨텐츠를 표시하도록 올바르게 구성됩니다.
