---
description: MediaPlayer 개체는 미디어 플레이어의 비헤이비어와 기능을 캡슐화합니다.
title: MediaPlayer 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# MediaPlayer 설정{#set-up-the-mediaplayer}

MediaPlayer 개체는 미디어 플레이어의 비헤이비어와 기능을 캡슐화합니다.

1. 인스턴스화 `MediaPlayer` 다음을 사용합니다.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 만들기 `MediaPlayerView` 인스턴스:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   위치 `container` 대상임 `div` 을 포함하는 요소 `HTMLMediaElement`.

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

   호출:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. 다음을 첨부합니다 `MediaPlayerView` 인스턴스: `MediaPlayer` 인스턴스:

   ```js
   player.view = view;
   ```

1. 사용자 지정 컨트롤 첨부 `div` 요소를 MediaPlayer 인스턴스에 추가합니다.

   예를 들어 HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   호출:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

다음 `MediaPlayer` 이제 인스턴스를 사용할 수 있으며 장치 화면에 비디오 콘텐츠를 표시하도록 올바르게 구성되었습니다.
