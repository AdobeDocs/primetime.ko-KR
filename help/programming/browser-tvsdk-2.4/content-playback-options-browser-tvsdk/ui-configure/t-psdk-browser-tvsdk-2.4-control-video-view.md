---
description: MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.
seo-description: MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.
seo-title: 비디오 보기의 위치 및 크기 제어
title: 비디오 보기의 위치 및 크기 제어
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 비디오 보기의 위치 및 크기 제어{#control-the-position-and-size-of-the-video-view}

MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.

브라우저 TVSDK는 애플리케이션, 프로필 스위치, 컨텐츠 스위치 등으로 인해 비디오 크기 또는 위치가 변경될 때마다 기본적으로 비디오 보기의 종횡비를 유지하려고 합니다.

다른 *비율 정책을*&#x200B;지정하여 기본 종횡비 동작을 재정의할 수 있습니다. 개체의 속성을 사용하여 비율 `MediaPlayerView` 정책을 지정합니다 `scalePolicy` . 의 기본 비율 정책은 `MediaPlayerView` 클래스의 `MaintainAspectRatioScalePolicy` 인스턴스로 설정됩니다. 비율 정책을 재설정하려면 기본 설정 `MaintainAspectRatioScalePolicy` 인스턴스를 `MediaPlayerView.scalePolicy` 사용자 지정 정책으로 바꿉니다.

>[!IMPORTANT]
>
>속성을 null 값으로 설정할 수 `scalePolicy` 없습니다.

## 비 Flash 폴백 시나리오 {#non-flash-fallback-scenarios}

Flash가 아닌 폴백 시나리오에서 크기 조절 정책이 올바르게 작동하려면 `View` 생성자에 지정된 비디오 div 요소가 `offsetWidth` 및 `offsetHeight`에 대해 0이 아닌 값을 반환해야 합니다. 잘못된 함수의 예를 제공하기 위해, 경우에 따라 비디오 div 요소의 너비와 높이가 css에 명시적으로 설정되지 않은 경우 `View` 생성자는 `offsetWidth` 또는 `offsetHeight`에 대해 0을 반환합니다.

>[!NOTE]
>
>CustomScalePolicy는 IE, Edge 및 Safari 9와 같은 일부 브라우저에 대한 지원을 제한적으로 제공합니다. 이러한 브라우저의 경우 비디오의 기본 종횡비를 변경할 수 없습니다. 그러나 비디오 위치와 크기는 비율 정책에 따라 적용됩니다.

1. 고유한 비율 정책을 만들려면 `MediaPlayerViewScalePolicy` 인터페이스를 구현합니다.

   여기에는 `MediaPlayerViewScalePolicy` 한 가지 방법이 있습니다.

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   예:

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. 속성에 구현을 할당합니다 `MediaPlayerView` .

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 보기를 Media Player의 `view` 속성에 추가합니다.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**예:종횡비를 유지하면서 전체 비디오 보기를 채우도록 비디오 크기를 조정합니다.**

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```

