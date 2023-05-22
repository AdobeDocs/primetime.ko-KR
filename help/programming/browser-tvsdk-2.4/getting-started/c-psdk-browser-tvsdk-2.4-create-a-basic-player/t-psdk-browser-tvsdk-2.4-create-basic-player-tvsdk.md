---
description: 브라우저 TVSDK를 사용하여 기본 플레이어를 만들려면 다음 단계를 완료하십시오.
title: TVSDK를 사용하여 기본 플레이어 만들기
exl-id: ea7485e0-5d15-469b-b8b6-f9604d283492
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# TVSDK를 사용하여 기본 플레이어 만들기{#create-a-basic-player-using-tvsdk}

브라우저 TVSDK를 사용하여 기본 플레이어를 만들려면 다음 단계를 완료하십시오.

1. Browser TVSDK용 압축 파일을 다운로드할 수 있는 새 디렉터리를 만듭니다.
1. Zendesk에서 브라우저 TVSDK를 다운로드하고 파일의 압축을 풀고 프레임워크 폴더를 새 디렉터리에 배치합니다.
1. 를 사용하여 코드에 대한 간단한 HTML 보일러판을 만듭니다. `div` 안에.
1. 1단계에서 만든 디렉터리의 HTML 파일에 이 보일러플레이트를 배치합니다.

   ```
   <!DOCTYPE html> 
   
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. 헤드 섹션에 브라우저 TVSDK 라이브러리를 추가합니다.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. body 태그의 경우 `onLoad` 섹션.

   ```
   <body onload="startVideo()">
   ```

1. 구현 시작 `startVideo` 함수.
1. 스크립트 태그를 추가하고 `startVideo` 태그에서 작동합니다.

   이것은 페이지의 헤드 섹션에 있어야 합니다.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. 만들기 `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 만들기 `MediaPlayerView`.

   >[!TIP]
   >
   >여기에서 `div` 이전에 만든 이 사용됩니다.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. 플레이어 이벤트 리스너를 추가합니다.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 이벤트 처리기를 구현하고 이를 이벤트 추가 리스너 앞에 추가합니다.

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
   
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   ```

1. 만들기 `MediaResource`M3U8 링크(또는 mpd)를 전달합니다.

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. 빈 구성을 만들고 리소스를 바꿉니다.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. 플레이어가 INITIALIZED 상태일 때 를 호출합니다. `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. 플레이어가 PREPARED 상태에 있으면 를 호출합니다. `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
