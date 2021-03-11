---
description: 배너 광고를 표시하려면 배너 인스턴스를 만들고 브라우저 TVSDK가 광고 관련 이벤트를 수신하도록 허용해야 합니다.
title: 배너 광고 표시
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 배너 광고 표시 {#display-banner-ads}

배너 광고를 표시하려면 배너 인스턴스를 만들고 브라우저 TVSDK가 광고 관련 이벤트를 수신하도록 허용해야 합니다.

브라우저 TVSDK는 `AdobePSDK.PSDKEventType.AD_STARTED` 이벤트를 통해 선형 광고와 연결된 부록 배너 광고 목록을 제공합니다.

매니페스트는 다음과 같은 방법으로 컴패니언 배너 광고를 지정할 수 있습니다.

* HTML 조각
* iFrame 페이지의 URL
* 정적 이미지 또는 Adobe Flash SWF 파일의 URL

각 관련 광고에 대해 브라우저 TVSDK는 애플리케이션에 사용 가능한 유형을 나타냅니다.

다음을 수행하는 이벤트 `AdobePSDK.PSDKEventType.AD_STARTED`에 대한 리스너를 추가합니다.
1. 배너 인스턴스에서 기존 광고를 지웁니다.
1. `Ad.getCompanionAssets`의 컴패니언 광고 목록을 가져옵니다.
1. 컴패니언 광고 목록이 비어 있지 않으면 배너 인스턴스 목록을 반복합니다.

   각 배너 인스턴스(`AdBannerAsset`)에는 폭, 높이, 리소스 유형(html, iframe 또는 static)과 같은 정보와 함께 사용 가능한 배너를 표시하는 데 필요한 데이터가 포함되어 있습니다.
1. 비디오 광고에 이와 함께 예약된 부록 광고가 없는 경우 컴패니언 자산 목록에는 해당 비디오 광고에 대한 데이터가 포함되어 있지 않습니다.
1. 배너를 적절한 위치에 표시하는 함수에 배너 정보를 보냅니다.

   일반적으로 `div`이고 사용자의 함수는 `div ID`를 사용하여 배너를 표시합니다. 예:

   이벤트 리스너를 추가합니다.

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   리스너 핸들러를 구현합니다.

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void 
   { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
            for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
                } 
            } 
        }  
        //...        
   }
   ```

   디스플레이를 처리하는 JavaScript 예:

   ```js
   function displayCompanion (resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
       var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
   
       // Assuming that there is an HTML element on the page  
       // with an id of "banner300x250", for example 
       if (bannerDiv !== null) { 
           bannerDiv.innerHTML = data; 
       } 
   }
   ```

