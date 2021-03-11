---
description: MediaPlayerView 객체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.
title: 비디오 보기의 위치 및 크기 제어
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# 비디오 보기{#control-the-position-and-size-of-the-video-view}의 위치와 크기를 제어합니다.

MediaPlayerView 객체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.

TVSDK는 기본적으로 비디오의 크기 또는 위치가 변경될 때마다(응용 프로그램, 프로필 스위치 또는 컨텐츠 전환 등으로 인해) 비디오 보기의 종횡비를 유지하려고 합니다.

다른 *비율 정책*&#x200B;을 지정하여 기본 종횡비 동작을 재정의할 수 있습니다. `MediaPlayerView` 개체의 `scalePolicy` 속성을 사용하여 비율 정책을 지정합니다. `MediaPlayerView`의 기본 비율 정책은 `MaintainAspectRatioScalePolicy` 클래스의 인스턴스로 설정됩니다. 비율 정책을 재설정하려면 `MediaPlayerView.scalePolicy`에 있는 `MaintainAspectRatioScalePolicy`의 기본 인스턴스를 자신의 정책으로 바꾸십시오. `scalePolicy` 속성은 null 값으로 설정할 수 없습니다.

1. `MediaPlayerViewScalePolicy` 인터페이스를 구현하여 고유한 비율 정책을 만듭니다.

   `MediaPlayerViewScalePolicy`에는 하나의 메서드가 있습니다.

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK는 `StageVideo` 개체를 사용하여 비디오를 표시하고 `StageVideo` 개체가 표시 목록에 없으므로 `viewPort` 매개 변수에는 비디오의 절대 좌표가 포함됩니다.
   >
   >
   >예:
   >
   >
   ```
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

1. 구현을 `MediaPlayerView` 속성에 할당합니다.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 보기를 미디어 플레이어의 `view` 속성에 추가합니다.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**예:종횡비를 유지하지 않고 전체 비디오 보기를 채우도록 비디오 크기를 조정합니다.**

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

