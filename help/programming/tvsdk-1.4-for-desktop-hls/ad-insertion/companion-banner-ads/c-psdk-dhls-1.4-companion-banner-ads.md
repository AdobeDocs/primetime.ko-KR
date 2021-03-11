---
description: TVSDK는 선형 광고를 수반하며 선형 광고가 끝난 후에도 종종 페이지에 유지되는 광고인 컴패니언 배너 광고를 지원합니다. 애플리케이션은 선형 광고와 함께 제공되는 부속 배너를 표시해야 합니다.
title: 컴패니언 배너 광고
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# 부록 배너 광고 {#companion-banner-ads}

TVSDK는 선형 광고를 수반하며 선형 광고가 끝난 후에도 종종 페이지에 유지되는 광고인 컴패니언 배너 광고를 지원합니다. 애플리케이션은 선형 광고와 함께 제공되는 부속 배너를 표시해야 합니다.

부록 광고를 표시할 때는 다음 권장 사항을 따르십시오.

* 플레이어의 레이아웃에 맞게 비디오 광고의 컴패니언 배너 광고를 최대한 표시하려고 합니다.
* 지정된 높이 및 폭과 정확히 일치하는 위치가 있는 경우에만 컴패니언 배너를 표시합니다.

   >[!TIP]
   >
   >배너 크기를 조정하지 마십시오.

* 광고가 시작된 후 가능한 한 빨리 컴패니언 배너를 제공합니다.
* 기본 광고/비디오 컨테이너와 함께 사용할 배너를 오버레이하지 마십시오.
* 광고가 끝난 후에도 계속 함께 배너를 표시합니다.

   이 배너를 대체하기 전까지 표준 배너는 각 컴패니언 배너를 표시합니다.

## 컴패니언 배너 데이터 {#companion-banner-data}

AdBannerAsset의 내용은 컴패니언 배너를 설명합니다.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`AdPlaybackEvent.AD_STARTED` 이벤트는 `companionAssets` 속성( `Vector.<AdAsset>`)이 포함된 `Ad` 인스턴스를 반환합니다.
각 `AdAsset`은 에셋 표시에 대한 정보를 제공합니다.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 사용 가능한 정보 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 너비 </td> 
   <td colname="col2"> 컴패니언 배너의 폭(픽셀 단위)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> 컴패니언 배너의 높이(픽셀 단위)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 리소스 유형 </td> 
   <td colname="col2">이 컴패니언 배너의 리소스 유형: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:데이터는 HTML 코드에 있습니다. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:데이터는 iframe URL(src)입니다. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 배너 데이터 </td> 
   <td colname="col2"> 이 컴패니언 배너에 대해 <span class="codeph"> resourceType</span>에서 지정한 유형의 데이터입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 정적 URL </td> 
   <td colname="col2"> <p>컴패니언 배너에는 이미지 또는 <span class="filepath"> .swf</span>(flash 배너)에 대한 직접 URL인 staticURL도 있을 수 있습니다. </p> <p>html 또는 iframe을 사용하지 않으려면 이미지 또는 swf에 대한 직접 URL을 사용하여 Flash 스테이지에 배너를 표시할 수 있습니다. 이 경우 staticURL을 사용하여 배너를 표시할 수 있습니다. </p> <p>중요: 정적 URL을 유효한 문자열인지 확인해야 합니다. 이 속성을 항상 사용할 수는 없기 때문입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 배너 광고 표시 {#display-banner-ads}

배너 광고를 표시하려면 배너 인스턴스를 만들고 TVSDK가 광고 관련 이벤트를 수신하도록 허용해야 합니다.

TVSDK는 `AdPlaybackEvent.AD_STARTED` 이벤트 이벤트를 통해 선형 광고와 연관된 컴패니언 배너 광고 목록을 제공합니다.

매니페스트는 다음과 같은 방법으로 컴패니언 배너 광고를 지정할 수 있습니다.

* HTML 조각
* iFrame 페이지의 URL
* 정적 이미지 또는 Adobe Flash SWF 파일의 URL

각 컴패니언 광고에 대해 TVSDK는 애플리케이션에 사용 가능한 유형을 나타냅니다.

다음을 수행하는 `AdPlaybackEvent.AD_STARTED` 이벤트에 대한 리스너를 추가합니다.

1. 배너 인스턴스에서 기존 광고를 지웁니다.

1. `Ad.companionAssets`의 컴패니언 광고 목록을 가져옵니다.

1. 컴패니언 광고 목록이 비어 있지 않으면 배너 인스턴스 목록을 반복합니다.

   각 배너 인스턴스( `AdBannerAsset`)에는 폭, 높이, 리소스 유형(html, iframe 또는 static)과 같은 정보와 함께 사용 가능한 배너를 표시하는 데 필요한 데이터가 포함되어 있습니다.

1. 비디오 광고에 이와 함께 예약된 부록 광고가 없는 경우 컴패니언 자산 목록에는 해당 비디오 광고에 대한 데이터가 포함되어 있지 않습니다.

   독립 실행형 디스플레이 광고를 표시하려면 해당 배너 인스턴스에 일반 DFP(발행자를 위한 DoubleClick)를 실행하는 논리를 스크립트에 추가합니다.

1. 배너를 적절한 위치에 표시하는 `ExternalInterface`을 사용하여 페이지의 함수인 JavaScript로 배너 정보를 보냅니다.

   일반적으로 `div`이고 사용자의 함수는 `div ID`를 사용하여 배너를 표시합니다. 예:

   이벤트 리스너를 추가합니다.

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   리스너 핸들러를 구현합니다.

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void { 
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
   function addBanner(resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
   
   //Assume an html element on the page with id like 'banner300x250' 
       var bannerDiv = document.getElementById('banner' + width +  
           'x' + height);  
       if (bannerDiv != null) { 
           if (resourceType == "html") { // for html resource 
               bannerDiv.innerHTML = data; 
           } 
           else if (resourceType == "iframe") { // for iframe resource 
               bannerDiv.innerHTML = "<iframe src='" + data +  
                   "' width='100%' height='100%'></iframe>"; 
           } 
       } 
   }
   ```
