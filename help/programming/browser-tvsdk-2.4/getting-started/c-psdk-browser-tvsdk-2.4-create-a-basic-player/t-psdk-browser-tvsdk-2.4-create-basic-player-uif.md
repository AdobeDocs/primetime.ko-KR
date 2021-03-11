---
title: UI 프레임워크를 사용하여 기본 플레이어 만들기
description: UI 프레임워크를 사용하여 기본 플레이어 만들기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# UI 프레임워크{#create-a-basic-player-using-the-ui-framework}을(를) 사용하여 기본 플레이어 만들기

UI 프레임워크를 사용하여 기본 플레이어를 만들려면:

1. 플레이어 인스턴스에 대해 `<div>`을 만듭니다.

   예:

   ```
   <div id="video1" > 
    </div>
   ```

1. 플레이어를 로드합니다.

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   플레이어가 만들어지면 지정된 `<div>` 요소에 `ptp-main-video-div-style`의 CSS 클래스가 지정됩니다. 결과 DOM은 다음과 같이 나타납니다.

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. UI 컨트롤을 추가합니다.

   예를 들어 마우스를 플레이어 위에 놓으면 나타나는 컨트롤 막대를 추가합니다.

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   결과 DOM은 다음과 같이 나타납니다.

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

호출에서 반환되는 개체는 TVSDK 미디어 플레이어 API를 래핑하는 비헤이비어를 제공하며 프로그래밍 방식으로 재생을 제어할 수 있도록 합니다. `ptp.videoPlayer()` 미디어 플레이어 인스턴스를 호출하면 사용자 인터페이스가 미디어 플레이어에서 실행하는 이벤트를 기반으로 자체적으로 업데이트됩니다.

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
