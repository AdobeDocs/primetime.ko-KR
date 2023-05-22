---
description: TVSDK는 클릭스루 광고에 대해 작업을 수행할 수 있도록 정보를 제공합니다. 플레이어 UI를 만들 때, 사용자가 클릭 가능한 광고를 클릭할 때 응답하는 방법을 결정해야 합니다.
title: 클릭 가능한 광고
exl-id: 50c74c82-c5d8-43f6-accf-8330a426a7bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 클릭 가능한 광고 {#clickable-ads}

TVSDK는 클릭스루 광고에 대해 작업을 수행할 수 있도록 정보를 제공합니다. 플레이어 UI를 만들 때, 사용자가 클릭 가능한 광고를 클릭할 때 응답하는 방법을 결정해야 합니다.

Flash 런타임용 TVSDK의 경우 선형 광고만 클릭할 수 있습니다.

## 광고 클릭에 응답 {#respond-to-clicks-on-ads}

사용자가 광고 또는 관련 버튼을 클릭하면 애플리케이션이 응답을 담당합니다. TVSDK는 대상 URL에 대한 정보를 제공합니다.

이 예에서는 광고 클릭을 관리하는 가능한 한 가지 방법을 보여 줍니다.

1. 광고가 재생될 때마다 미디어 플레이어 위에 단추를 표시합니다. 광고를 클릭한 사용자는 광고 URL로 리디렉션됩니다. 이 단추는 [!DNL ClickableAdsOverlay.xml].

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. 미디어 플레이어 샘플에 이 오버레이를 포함하십시오. [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. 광고가 재생될 때만 보기를 표시하려면 다음 내용을 수신 대기하십시오. `onAdStart` 및 `onAdComplete` 에서 발송한 이벤트.

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. 클릭 가능한 광고에서 사용자 상호 작용을 모니터링합니다. 사용자가 광고 또는 버튼을 터치하거나 클릭할 때 TVSDK에 다음과 같이 알립니다. `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. 다음을 들어보십시오. `AdclickEvent.AD_CLICK` 이벤트.

   광고가 재생되는 경우 TVSDK가 `AdClickEvent.AD_CLICK` 클릭스루 URL 및 관련 정보를 검색할 수 있는 이벤트입니다.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. 사용자를 광고 URL로 안내하는 동안 미디어 플레이어를 일시 중지합니다.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. 광고 클릭스루 URL 및 관련 정보를 표시합니다.

       예를 들어 다음 방법 중 하나로 표시할 수 있습니다.
   
   * 애플리케이션 내의 브라우저에서 클릭스루 URL을 엽니다.

      데스크탑 플랫폼에서는 일반적으로 비디오 광고 재생 영역을 사용자 클릭 시 클릭스루 URL을 호출하는 데 사용합니다.
   * 사용자를 외부 모바일 웹 브라우저로 리디렉션합니다.

      모바일 장치에서 비디오 광고 재생 영역은 컨트롤 숨기기 및 표시, 재생 일시 중지, 전체 화면으로 확장 등의 다른 기능에 사용됩니다. 따라서 모바일 장치에서는 일반적으로 스폰서 버튼과 같은 별도의 보기가 클릭스루 URL을 시작하는 수단으로 사용자에게 표시됩니다.

1. 클릭스루 정보가 표시되는 브라우저 창을 닫고 비디오 재생을 재개합니다.
