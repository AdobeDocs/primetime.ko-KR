---
description: MediaPlayer는 클릭 가능한 광고가 재생될 때 광고 관련 이벤트를 전달하는 notifyClick() 함수를 제공합니다. 이러한 이벤트는 앱에서 클릭스루 기능을 제공하는 데 사용할 수 있는 광고 및 광고 중단 정보를 제공합니다.
seo-description: MediaPlayer는 클릭 가능한 광고가 재생될 때 광고 관련 이벤트를 전달하는 notifyClick() 함수를 제공합니다. 이러한 이벤트는 앱에서 클릭스루 기능을 제공하는 데 사용할 수 있는 광고 및 광고 중단 정보를 제공합니다.
seo-title: 클릭 가능한 광고 처리
title: 클릭 가능한 광고 처리
uuid: 5d3c9d36-60d7-4272-a523-7d1fe0e1615f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 클릭 가능한 광고 {#handle-clickable-ads} 처리

MediaPlayer는 클릭 가능한 광고가 재생될 때 광고 관련 이벤트를 전달하는 notifyClick() 함수를 제공합니다. 이러한 이벤트는 앱에서 클릭스루 기능을 제공하는 데 사용할 수 있는 광고 및 광고 중단 정보를 제공합니다.

클릭 가능한 광고가 재생될 때 MediaPlayer는 다음 이벤트를 실행합니다.

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

`AdClickedEvent`에는 클릭스루 함수를 처리하는 데 필요한 정보가 포함되어 있습니다.

1. 사용자가 클릭 가능한 광고를 클릭할 수 있도록 플레이어에서 컨트롤을 제공합니다.

   사용자의 클릭을 캡처하는 단추 또는 기타 요소일 수 있습니다.
1. 사용자의 광고 클릭 이벤트에 대한 이벤트 리스너를 추가합니다.

   예:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. 사용자의 클릭 이벤트에 대한 핸들러를 추가합니다.

   이 핸들러는 MediaPlayer에서 `AdClicked` 이벤트를 실행할지 여부를 묻는 메시지를 표시해야 합니다.

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   ```

1. MediaPlayer 광고 시작, 클릭 및 완성된 알림에 대한 이벤트 리스너를 추가합니다.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. 이벤트 핸들러를 추가합니다.
a.광고 시작 이벤트를 처리합니다.
이 경우 사용자에 대한 UI 설정과 같은 모든 작업을 수행할 수 있습니다.

   ```
   onAdStarted = function (event) { 
       if (clickAddButton && event && event.ad) { 
           var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           if (adClick && adClick.isValid) { 
               // Do some initial processing  
               // when the ad starts, prior 
               // to the user's click. 
           } 
       } 
   }
   ```

   b.클릭한 광고를 처리합니다.
이 예에서는 이벤트에서 광고 정보를 얻고 해당 정보를 사용하여 새 브라우저 창을 엽니다.

   ```
   onAdClickedEvent = function (event) { 
       if (event && event.ad) { 
           var adClick = event.adClick; 
           if (!(adClick && adClick.isValid)) { 
               adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           } 
           if (adClick && adClick.isValid) 
           { 
               // Do something with the currently playing ad 
               window.open(adClick.url); 
           } 
       } 
   }
   ```

   c. 광고 완료 이벤트를 처리합니다.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
