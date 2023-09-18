---
description: MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.
title: 비디오 보기의 위치 및 크기 제어
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 비디오 보기의 위치 및 크기 제어{#control-the-position-and-size-of-the-video-view}

MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.

TVSDK는 기본적으로 비디오 크기나 위치가 변경될 때마다(애플리케이션이나 프로필 스위치, 콘텐츠 스위치 등의 변경으로 인해) 비디오 보기의 종횡비를 유지합니다.

다른 값을 지정하여 기본 종횡비를 재정의할 수 있습니다 *정책 확장*. 다음을 사용하여 크기 조정 정책 지정 `MediaPlayerView` 개체 `scalePolicy` 속성. 다음 `MediaPlayerView`의 기본 크기 조정 정책은 의 인스턴스로 설정됩니다. `MaintainAspectRatioScalePolicy` 클래스. 크기 조정 정책을 재설정하려면 의 기본 인스턴스를 `MaintainAspectRatioScalePolicy` 날짜 `MediaPlayerView.scalePolicy` 자체 정책 사용. (다음을 설정할 수 없습니다. `scalePolicy` 속성을 null 값으로 설정합니다.)

1. 구현 `MediaPlayerViewScalePolicy` 고유한 크기 조정 정책을 만드는 인터페이스입니다.

   다음 `MediaPlayerViewScalePolicy` 에는 한 가지 방법이 있습니다.

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK는 `StageVideo` 비디오 표시 개체 및 이유 `StageVideo` 표시 목록에 없는 개체 `viewPort` 매개 변수에는 비디오의 절대 좌표가 포함됩니다.
   >
   >
   >예:
   >
   >```
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >       /** 
   >         * Default constructor. 
   >         */ 
   >       public function CustomScalePolicy() { 
   >       } 
   > 
   >    
      public function adjust(viewPort:Rectangle,  
   >                                                     videoWidth:Number,  
   >                                                     videoHeight:Number):Rectangle { 
   >               return customAdjustment(); 
   >       } 
   > 
   >    
      public function customAdjustment():Rectangle { 
   >               /* Your custom adjustment here */ 
   >               [...] 
   >       } 
   >}
   >```
   >

1. 에 구현 할당 `MediaPlayerView` 속성.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 미디어 플레이어의 보기에 추가 `view` 속성.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**예를 들어 종횡비를 유지하지 않고 전체 비디오 보기를 채우도록 비디오 크기를 조정합니다.**

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```
