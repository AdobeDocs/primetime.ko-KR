---
description: 브라우저 TV SDK를 사용하여 기본 플레이어를 만들려면 다음 단계를 수행하십시오.
title: TVSDK를 사용하여 기본 플레이어 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# TVSDK{#create-a-basic-player-using-tvsdk}를 사용하여 기본 플레이어 만들기

브라우저 TV SDK를 사용하여 기본 플레이어를 만들려면 다음 단계를 수행하십시오.

1. 브라우저 TVSDK용 압축 파일을 다운로드할 수 있는 새 디렉토리를 만듭니다.
1. Zendesk에서 브라우저 TV SDK를 다운로드하고, 파일의 압축을 풀고, frameworks 폴더를 새 디렉토리에 넣습니다.
1. 코드에 `div`이 포함된 간단한 HTML 상용구를 만듭니다.
1. 1단계에서 만든 디렉토리에 이 상용구를 HTML 파일에 배치합니다.

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

1. 헤드 섹션에 브라우저 TV SDK 라이브러리를 추가합니다.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. body 태그의 경우 `onLoad` 섹션을 추가합니다.

   ```
   <body onload="startVideo()">
   ```

1. `startVideo` 함수 구현을 시작합니다.
1. 스크립트 태그를 추가하고 태그에 `startVideo` 함수를 만듭니다.

   페이지의 헤드 섹션에 있어야 합니다.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. `Adobe.MediaPlayer`을(를) 만듭니다.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. `MediaPlayerView`을(를) 만듭니다.

   >[!TIP]
   >
   >여기에서 이전에 만든 `div`이 사용됩니다.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. 플레이어 이벤트 리스너를 추가합니다.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 이벤트 핸들러를 구현하고 이를 add 이벤트 리스너 앞에 놓습니다.

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

1. M3U8 링크(또는 mpd)를 전달하는 `MediaResource`을 만듭니다.

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

1. 플레이어가 초기화된 상태이면 `prepareToPlay`을(를) 호출합니다.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. 플레이어가 준비 상태가 되면 `play`으로 전화하십시오.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

