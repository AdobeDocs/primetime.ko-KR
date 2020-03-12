---
description: MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.
seo-description: MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.
seo-title: 비디오 보기의 위치 및 크기 제어
title: 비디오 보기의 위치 및 크기 제어
uuid: 2231c574-03cd-45a8-ab00-4a42f8e044f0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 비디오 보기의 위치 및 크기 제어{#control-the-position-and-size-of-the-video-view}

MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.

TVSDK는 기본적으로 비디오의 크기 또는 위치가 변경될 때마다(응용 프로그램, 프로필 전환 또는 컨텐츠 전환 등으로 인해) 비디오 보기의 종횡비를 유지합니다.

다른 *비율 정책을*&#x200B;지정하여 기본 종횡비 동작을 재정의할 수 있습니다. 개체의 속성을 사용하여 비율 `MediaPlayerView` 정책을 지정합니다 `scalePolicy` . 기본 비율 `MediaPlayerView`정책은 `MaintainAspectRatioScalePolicy` 클래스의 인스턴스로 설정됩니다. 비율 정책을 재설정하려면 기본 설정 `MaintainAspectRatioScalePolicy` 인스턴스를 `MediaPlayerView.scalePolicy` 사용자 지정 정책으로 바꿉니다. (속성을 null 값으로 설정할 수 `scalePolicy` 없습니다.)

1. 고유한 비율 정책을 만들려면 `MediaPlayerViewScalePolicy` 인터페이스를 구현합니다.

   여기에는 `MediaPlayerViewScalePolicy` 한 가지 방법이 있습니다.

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK는 비디오를 표시하기 위해 `StageVideo` 개체를 사용하며 `StageVideo` 개체가 표시 목록에 없으므로 `viewPort` 매개 변수에는 비디오의 절대 좌표가 포함됩니다.
   >
   >
   >예:   >
   >
   >
   ```>
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
   >```   >
   >



1. 속성에 구현을 할당합니다 `MediaPlayerView` .

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 보기를 Media Player의 `view` 속성에 추가합니다.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**예:종횡비를 유지하면서 전체 비디오 보기를 채우도록 비디오 크기를 조정합니다.**

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

