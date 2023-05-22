---
title: UI 프레임워크를 사용하여 기본 플레이어 만들기
description: UI 프레임워크를 사용하여 기본 플레이어 만들기
copied-description: true
exl-id: 78629042-fd87-406b-af42-229e34d48162
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# UI 프레임워크를 사용하여 기본 플레이어 만들기{#create-a-basic-player-using-the-ui-framework}

UI 프레임워크를 사용하여 기본 플레이어를 만들려면 다음 작업을 수행하십시오.

1. 만들기 `<div>` 플레이어 인스턴스에 사용됩니다.

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

   플레이어가 만들어지면 `<div>` 요소에 다음의 CSS 클래스가 제공됩니다. `ptp-main-video-div-style`. 결과 DOM은 다음과 같이 나타납니다.

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. UI 컨트롤을 추가합니다.

   예를 들어, 마우스로 플레이어를 가리키면 표시되는 컨트롤 막대를 추가합니다.

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

호출에서 반환된 개체 `ptp.videoPlayer()` 는 TVSDK 미디어 플레이어 API를 래핑하고 프로그래밍 방식으로 재생을 제어할 수 있는 비헤이비어를 제공합니다. 미디어 플레이어 인스턴스를 호출하면 미디어 플레이어에서 실행된 이벤트를 기반으로 사용자 인터페이스가 업데이트됩니다.

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
