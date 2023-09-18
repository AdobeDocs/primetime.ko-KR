---
description: TVSDK는 컴패니언 배너 광고를 지원합니다. 광고는 선형 광고와 함께 제공되며, 선형 광고가 끝난 후에도 페이지에 남아 있는 경우가 많은 광고입니다. 애플리케이션은 선형 광고와 함께 제공되는 컴패니언 배너를 표시할 책임이 있습니다.
title: 컴패니언 배너 광고
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 컴패니언 배너 광고 {#companion-banner-ads}

TVSDK는 컴패니언 배너 광고를 지원합니다. 광고는 선형 광고와 함께 제공되며, 선형 광고가 끝난 후에도 페이지에 남아 있는 경우가 많은 광고입니다. 애플리케이션은 선형 광고와 함께 제공되는 컴패니언 배너를 표시할 책임이 있습니다.

컴패니언 광고를 표시할 때에는 다음 권장 사항을 따르십시오.

* 플레이어의 레이아웃에 맞게 비디오 광고의 컴패니언 배너 광고를 최대한 많이 표시하십시오.
* 지정한 높이 및 너비와 정확히 일치하는 위치가 있는 경우에만 컴패니언 배너를 표시합니다.

  >[!TIP]
  >
  >배너의 크기를 조정하지 마십시오.

* 광고가 시작된 후 가능한 한 빨리 컴패니언 배너를 표시합니다.
* 기본 광고/비디오 컨테이너를 컴패니언 배너와 오버레이하지 마십시오.
* 광고가 끝난 후에도 계속 동반 배너를 표시합니다.

  표준은 이 배너를 교체할 때까지 각 컴패니언 배너를 표시하는 것입니다.

## 컴패니언 배너 데이터 {#companion-banner-data}

AdBannerAsset의 콘텐츠는 컴패니언 배너에 대해 설명합니다.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

다음 `AdPlaybackEvent.AD_STARTED` 이벤트가 다음을 반환합니다. `Ad` 이 포함된 인스턴스 `companionAssets` 속성( `Vector.<AdAsset>`).
각 `AdAsset` 에셋 표시에 대한 정보를 제공합니다.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 사용 가능한 정보 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 폭 </td> 
   <td colname="col2"> 컴패니언 배너의 픽셀 단위 폭입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 높이 </td> 
   <td colname="col2"> 컴패니언 배너의 픽셀 단위 높이입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 리소스 유형 </td> 
   <td colname="col2">이 컴패니언 배너의 리소스 유형: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: 데이터가 HTML 코드에 있습니다. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: 데이터가 iframe URL(src)입니다. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 배너 데이터 </td> 
   <td colname="col2"> 에 지정된 유형의 데이터 <span class="codeph"> resourceType</span> 이 컴패니언 배너용. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 정적 URL </td> 
   <td colname="col2"> <p>경우에 따라 컴패니언 배너에는 이미지 또는 의 직접 URL인 staticURL도 있습니다 <span class="filepath"> .swf</span> (Flash 배너). </p> <p>html 또는 iframe을 사용하지 않으려면 이미지나 swf에 대한 직접 URL을 사용하여 Flash 단계에 배너를 대신 표시할 수 있습니다. 이 경우 staticURL을 사용하여 배너를 표시할 수 있습니다. </p> <p>중요: 이 속성을 항상 사용할 수 있는 것은 아니므로 정적 URL이 유효한 문자열인지 확인해야 합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 배너 광고 표시 {#display-banner-ads}

배너 광고를 표시하려면 배너 인스턴스를 만들고 TVSDK가 광고 관련 이벤트를 수신하도록 해야 합니다.

TVSDK는 를 통해 선형 광고와 연결된 컴패니언 배너 광고 목록을 제공합니다. `AdPlaybackEvent.AD_STARTED` 이벤트 이벤트.

매니페스트는 다음과 같은 방법으로 컴패니언 배너 광고를 지정할 수 있습니다.

* HTML 코드 조각
* iFrame 페이지의 URL
* 정적 이미지 또는 Adobe Flash SWF 파일의 URL

각 컴패니언 광고에 대해 TVSDK는 애플리케이션에 사용할 수 있는 유형을 나타냅니다.

다음에 대한 리스너 추가 `AdPlaybackEvent.AD_STARTED` 다음을 수행하는 이벤트:

1. 배너 인스턴스에서 기존 광고를 지웁니다.

1. 에서 컴패니언 광고 목록을 가져옵니다. `Ad.companionAssets`.

1. 컴패니언 광고 목록이 비어 있지 않으면 배너 인스턴스 목록을 반복합니다.

   각 배너 인스턴스( `AdBannerAsset`)에는 너비, 높이, 리소스 유형(html, iframe 또는 정적) 및 컴패니언 배너를 표시하는 데 필요한 데이터와 같은 정보가 포함되어 있습니다.

1. 비디오 광고에 그와 함께 예약된 컴패니언 광고가 없는 경우, 컴패니언 자산 목록에는 해당 비디오 광고에 대한 데이터가 없습니다.

   독립 실행형 디스플레이 광고를 표시하려면 스크립트에 논리를 추가하여 적절한 배너 인스턴스에서 일반 DFP(게시자용 DoubleClick) 디스플레이 태그를 실행합니다.

1. 를 사용하여 배너 정보를 페이지의 함수(일반적으로 JavaScript)에 보냅니다. `ExternalInterface`를 입력하면 배너가 적절한 위치에 표시됩니다.

   이는 일반적으로 `div`및 함수를 호출하면 함수에서 `div ID` 배너를 표시합니다. 예:

   이벤트 리스너 추가:

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

   디스플레이를 처리하는 JavaScript의 예:

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
