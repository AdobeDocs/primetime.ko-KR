---
description: 브라우저 TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.
title: 비디오의 지속 시간, 현재 시간 및 남은 시간을 표시합니다.
exl-id: f2aa3c42-9c47-4a55-aed6-7dc5a8d0662b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# 비디오의 지속 시간, 현재 시간 및 남은 시간을 표시합니다.{#display-the-duration-current-time-and-remaining-time-of-the-video}

브라우저 TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.

1. 플레이어가 적어도 PREPARED 상태가 될 때까지 기다립니다.
1. 를 사용하여 현재 플레이헤드 시간 검색 `MediaPlayer.currentTime` 특성.

   이 속성은 가상 타임라인의 현재 플레이헤드 위치를 밀리초 단위로 반환합니다. 이 시간은 기본 스트림에 여러 광고 또는 광고 브레이크와 같은 대체 콘텐츠의 여러 인스턴스를 포함할 수 있는 확인된 스트림을 기준으로 계산됩니다. 라이브/선형 스트림의 경우 반환되는 시간은 항상 재생 창 범위입니다.

   ```js
   MediaPlayer.currentTime
   ```

1. 스트림의 재생 범위를 검색하고 지속 시간을 결정합니다.
   1. 사용  `mediaPlayer.playbackRange` 속성을 사용하여 가상 타임라인 시간 범위를 가져올 수 있습니다.

   1. 기간을 결정하려면 범위의 끝에서 시작을 뺍니다.

      여기에는 스트림(광고)에 삽입되는 추가 콘텐츠 지속 시간이 포함됩니다.

      VOD의 경우 범위는 항상 0으로 시작하며 종료 값은 기본 콘텐츠 지속 시간과 스트림(광고)에 삽입된 추가 콘텐츠 지속 시간의 합계와 같습니다.

      선형/라이브 에셋의 경우 범위는 재생 창 범위를 나타내며 이 범위는 재생 중에 변경됩니다.

1. MediaPlayer 및 브라우저 TVSDK 요소에서 사용할 수 있는 메서드를 사용하여 검색 막대 매개 변수를 설정합니다.

   예를 들어 HTML 시 검색 막대를 표시할 수 있는 레이아웃이 있습니다.

   ```
   <div class="seekbar" id="seekbar"> 
        <div> 
           <span class="backer" id="backer"></span> 
           <span class="buffer" id="buffer" ></span> 
           <div class="playhead" id="playhead"></div> 
                     <span class="progress" id="progress" ></span> 
           </div> 
         </div> 
     </div> 
   ```

   다음은 해당 css입니다.

   ```
   #seekbar { 
         position: relative; 
         width: 100%; 
         height: 16px; 
         cursor: pointer; 
         background: transparent; 
   } 
   
   #seekbar div { 
         position: relative; 
         height: 100%; 
         margin-left: 8px; 
         margin-right: 8px; 
   } 
   
   #seekbar span { 
         position: absolute; 
         height: 60%; 
         top: 20%; 
   
         display: block; 
   
         -webkit-border-radius: 16px; 
         -moz-border-radius: 16px; 
         border-radius: 16px; 
   } 
   
   #seekbar.playhead { 
        z-index: 1011; 
        height: 14px; 
        width: 14px; 
        border: 1px outset #c9cbce; 
        position: absolute; 
        left: -8px; /* adjust center of playhead over start of range */ 
        display: block; 
        padding: 0; 
        margin: 0; 
   
        background: #c9cbce; /* Old browsers */ 
        background: -moz-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* FF3.6+ */ 
        background: -webkit-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* Chrome10+,Safari5.1+ */ 
        background: -o-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* Opera 11.10+ */ 
        background: -ms-radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* IE10+ */ 
        background: radial-gradient(circle, #4591ce 0%, #3080c2 40%, #c9cbce 45%, #dedee1 100%); /* W3C */ 
        filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#c9cbce', endColorstr='#dedee1',GradientType=0 ); /* IE6-9 */ 
   
        -webkit-border-radius: 16px; 
        -moz-border-radius: 16px; 
        border-radius: 16px; 
   } 
   
   #seekbar.backer { 
           z-index: 1004; 
           width: 100%; 
   
           background: #414142; /* Old browsers */ 
           background: -moz-linear-gradient(top,  #414142 0%, #343232 100%); /* FF3.6+ */ 
           background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#414142), color-stop(100%,#343232)); /* Chrome,Safari4+ */ 
           background: -webkit-linear-gradient(top,  #414142 0%,#343232 100%); /* Chrome10+,Safari5.1+ */ 
           background: -o-linear-gradient(top,  #414142 0%,#343232 100%); /* Opera 11.10+ */ 
           background: -ms-linear-gradient(top,  #414142 0%,#343232 100%); /* IE10+ */ 
           background: linear-gradient(to bottom,  #414142 0%,#343232 100%); /* W3C */ 
           filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#414142', endColorstr='#343232',GradientType=0 ); /* IE6-9 */ 
   
   } 
   
   #seekbar .buffer { 
          z-index: 1005; 
          position: absolute; 
   
          background: #4b4b4c; /* Old browsers */ 
          background: -moz-linear-gradient(top,  #4b4b4c 0%, #818184 100%); /* FF3.6+ */ 
          background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#4b4b4c), color-stop(100%,#818184)); /* Chrome,Safari4+ */ 
          background: -webkit-linear-gradient(top,  #4b4b4c 0%,#818184 100%); /* Chrome10+,Safari5.1+ */ 
          background: -o-linear-gradient(top,  #4b4b4c 0%,#818184 100%); /* Opera 11.10+ */ 
          background: -ms-linear-gradient(top,  #4b4b4c 0%,#818184 100%); /* IE10+ */ 
          background: linear-gradient(to bottom,  #4b4b4c 0%,#818184 100%); /* W3C */ 
          filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#4b4b4c', endColorstr='#818184',GradientType=0 ); /* IE6-9 */ 
   } 
   
   #seekbar .progress { 
           z-index: 1010; 
           position: absolute; 
   
           background: #4591ce; /* Old browsers */ 
           background: -moz-linear-gradient(top,  #4591ce 0%, #3080c2 100%); /* FF3.6+ */ 
           background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#4591ce), color-stop(100%,#3080c2)); /* Chrome,Safari4+ */ 
           background: -webkit-linear-gradient(top,  #4591ce 0%,#3080c2 100%); /* Chrome10+,Safari5.1+ */ 
           background: -o-linear-gradient(top,  #4591ce 0%,#3080c2 100%); /* Opera 11.10+ */ 
           background: -ms-linear-gradient(top,  #4591ce 0%,#3080c2 100%); /* IE10+ */ 
           background: linear-gradient(to bottom,  #4591ce 0%,#3080c2 100%); /* W3C */ 
           filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#4591ce', endColorstr='#3080c2',GradientType=0 ); /* IE6-9 */ 
   } 
   ```

1. 잘 들어 `AdobePSDK.TimeChangeEvent` 및 그에 따라 seekbar를 업데이트합니다.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIME_CHANGED, onTimeChange); 
   
   /** 
        * Called when the player's time changes. 
        * Update UI to show current time, seekbar playhead position and buffer level. 
        */ 
        function onTimeChange(event) 
        { 
          if (!seekBar.isSeeking) { 
          var time = event.time; 
          var range = player.playbackRange; 
          seekBar.updatePlayhead(time, range); 
          updateDisplayTime(time, range); 
   
           var bufferedRange = player.bufferedRange; 
           seekBar.updateBufferLevel(bufferedRange.end, range); 
         } 
   
       } 
   ```

   다음 예제에서는 seekbar 개체를 만들어 seekbar를 업데이트합니다.

   ```js
   /** 
       * Seekbar object which handles the display of the player progress,  
       * playhead, and buffer level. 
       */ 
       seekBar = (function () { 
   
       var playheadHalfSize = 8, // must be half width of playhead defined in CSS 
           containerElm = null, 
           playheadElm = null, 
           backerElm = null, 
           bufferElm = null, 
           progressElm = null, 
           currentPos = 0, // [0,1] relative to range 
           currentBuffer = 0,// [0,1] relative to range 
           listener = null, 
           isSeeking = false, 
   
            setPositionChangeListener = function (funct) { 
               listener = funct; 
            }, 
   
            getSeekBarBounds = function () { 
              return backerElm.getBoundingClientRect(); 
            }, 
   
            onPositionChange = function (event) { 
                var pos = event.pageX || event.clientX; 
                var bounds = getSeekBarBounds(); 
                // normalize position to seek bounds 
                pos -= bounds.left; 
                var percent = pos / (bounds.right - bounds.left); 
   
                // check bounds 
                 if (percent > 1) percent = 1; 
                 else if (percent < 0) percent = 0; 
   
                 currentPos = percent; 
                 setPosition(percent); 
              }, 
   
                 updatePlayhead = function (time, range) { 
                 if (!isSeeking) { 
                 var pos = convertTimeToRelativePosition(time, range); 
                 setPosition(pos); 
              } 
            }, 
   
               setPosition = function (percent) { 
               // adjust to keep playhead graphic inside container on right side 
               var bounds = getSeekBarBounds(); 
               var pos = percent * (bounds.right - bounds.left); 
   
               progressElm.style.width = (pos).toString() + "px"; 
               playheadElm.style.left = (pos-playheadHalfSize).toString() + "px"; 
   
               currentPos = percent; 
               return percent; 
   
               }, 
   
                updateBufferLevel = function (level, range) { 
                if (!isSeeking) { 
                    var position = convertTimeToRelativePosition(level, range); 
                    setBufferLevel(position); 
                   } 
               }, 
   
                 setBufferLevel = function (percent) { 
                    currentBuffer = percent; 
                    var bounds = getSeekBarBounds(); 
                    var pos = percent * (bounds.right - bounds.left); 
   
                           bufferElm.style.width = pos.toString() + "px"; 
                       }, 
   
                       resetSeekBar = function () { 
                          setPosition(currentPos); 
                          setBufferLevel(currentBuffer); 
                       }, 
   
                       convertTimeToRelativePosition = function (time, range) { 
                          // convert time to a percentage of the duration 
                          var position = (time - range.begin) / range.duration; 
                          if (position > 1) position = 1; 
                          else if (position < 0) position = 0; 
                          return position; 
                       }, 
   
                       unattachEvents = function (e) { 
                         this.removeEventListener('mousemove', onPositionChange); 
                         this.removeEventListener('mouseout', unattachEvents); 
                         this.removeEventListener('mouseup', unattachEvents); 
   
                           this.addEventListener('mouseover', attachEvents); 
                           isSeeking = false; 
                       }, 
   
                       attachEvents = function (e) { 
                          this.addEventListener('mousemove', onPositionChange); 
                          this.addEventListener('mouseout', unattachEvents); 
                          this.addEventListener('mouseup', unattachEvents); 
                          isSeeking = true; 
                          return false; 
                       }; 
   
               return  { 
                   init : function () { 
                     containerElm = document.getElementById("seekbar"); 
                     backerElm = document.getElementById("backer"); 
                     playheadElm = document.getElementById("playhead"); 
                     bufferElm = document.getElementById("buffer"); 
                     progressElm = document.getElementById("progress"); 
   
                     // client seek via scrubbing 
                     containerElm.addEventListener('mousedown', attachEvents); 
   
                     // client seek via single click or 'mouseup' after scrubbing 
                     containerElm.addEventListener('click', function (e) { 
                        if (listener !== null && !player.areControlsDisabledInAd()) { 
                           onPositionChange(e); 
                           // callback to notify of desired seek position 
                           listener.call(this, currentPos); 
                           } 
                       }); 
   
                       // end client seek via scrubbing 
                       document.addEventListener('mouseup', function (e) { 
                           containerElm.removeEventListener('mouseover', attachEvents); 
                       }); 
                   }, 
   
                  /** 
                  * Is the playhead currently being scrubbed. 
                  */ 
                  isSeeking : isSeeking, 
   
                  /** 
                  * Change the position of the playhead. 
                  * @param time - time in seconds to position playhead 
                  * @param range - current playback range 
                  */ 
                  updatePlayhead : updatePlayhead, 
   
                  /** 
                  * Change the position of the buffer range. 
                  * @param time - time in seconds to position head of buffer 
                  * @param range - current playback range 
                  */ 
                  updateBufferLevel : updateBufferLevel, 
   
                  /** 
                  * Set listener which is called when the playhead position changes 
                  * by the user event. Listener is not called when playhead position 
                  * changes via updatePlayhead function. 
                  * @param listener - callback function, passed single position argument 
                  * representing the playhead position in the range [0,1]. 
                  */ 
                  setPositionChangeListener : setPositionChangeListener, 
   
                  /** 
                  * Readjust position levels if seekbar is resized. 
                  * Should be called every time the video window changes size. 
                  */ 
                  readjustSeekBar : resetSeekBar 
               }; 
   
           })(); 
   ```
