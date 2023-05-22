---
description: MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.
title: 비디오 보기의 위치 및 크기 제어
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 비디오 보기의 위치 및 크기 제어{#control-the-position-and-size-of-the-video-view}

MediaPlayerView 개체를 사용하여 비디오 보기의 위치와 크기를 제어할 수 있습니다.

브라우저 TVSDK는 기본적으로 애플리케이션, 프로필 스위치, 콘텐츠 스위치 등의 변경으로 인해 비디오의 크기나 위치가 변경될 때마다 비디오 보기의 종횡비를 유지하려고 합니다.

다른 값을 지정하여 기본 종횡비를 재정의할 수 있습니다 *정책 확장*. 다음을 사용하여 크기 조정 정책 지정 `MediaPlayerView` 개체 `scalePolicy` 속성. 의 기본 크기 조정 정책 `MediaPlayerView` 의 인스턴스로 설정됩니다. `MaintainAspectRatioScalePolicy` 클래스. 크기 조정 정책을 재설정하려면 의 기본 인스턴스를 `MaintainAspectRatioScalePolicy` 날짜 `MediaPlayerView.scalePolicy` 자체 정책 사용.

>[!IMPORTANT]
>
>다음을 설정할 수 없습니다. `scalePolicy` 속성을 null 값으로 설정합니다.

## Flash이 아닌 대체 시나리오 {#non-flash-fallback-scenarios}

Flash이 아닌 대체 시나리오에서 배율 정책이 올바르게 작동하려면 다음 위치에 비디오 div 요소를 지정합니다. `View` 생성자는 다음에 대해 0이 아닌 값을 반환해야 합니다. `offsetWidth` 및 `offsetHeight`. 잘못된 함수의 예를 제공하기 위해 비디오 div 요소의 너비와 높이가 css에서 명시적으로 설정되지 않은 경우 `View` 생성자가 다음에 대해 0을 반환합니다. `offsetWidth` 또는 `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy에서는 IE, Edge 및 Safari 9와 같은 몇 가지 브라우저에 대한 지원이 제한되었습니다. 이러한 브라우저의 경우 비디오의 기본 종횡비를 변경할 수 없습니다. 그러나 비디오의 위치와 차원은 규모 정책에 따라 시행됩니다.

1. 구현 `MediaPlayerViewScalePolicy` 고유한 크기 조정 정책을 만드는 인터페이스입니다.

   다음 `MediaPlayerViewScalePolicy` 에는 한 가지 방법이 있습니다.

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

1. 에 구현 할당 `MediaPlayerView` 속성.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 미디어 플레이어의 보기에 추가 `view` 속성.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**예를 들어 종횡비를 유지하지 않고 전체 비디오 보기를 채우도록 비디오 크기를 조정합니다.**

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
