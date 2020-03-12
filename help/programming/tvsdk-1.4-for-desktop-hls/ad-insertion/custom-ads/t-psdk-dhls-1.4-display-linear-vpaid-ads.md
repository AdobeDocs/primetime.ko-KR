---
description: TVSDK 파섹 VPAID 버전 1.0을 사용하려면 Flash가 필요하고 버전 2.0은 Browser TVSDK 및 JavaScript에서도 작동합니다.
seo-description: TVSDK 파섹 VPAID 버전 1.0을 사용하려면 Flash가 필요하고 버전 2.0은 Browser TVSDK 및 JavaScript에서도 작동합니다.
seo-title: 광고 중단으로 선형 VPAID 광고 표시
title: 광고 중단으로 선형 VPAID 광고 표시
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 광고 중단으로 선형 VPAID 광고 표시{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK 파섹 VPAID 버전 1.0을 사용하려면 Flash가 필요하고 버전 2.0은 Browser TVSDK 및 JavaScript에서도 작동합니다.

VPAID 광고를 올바로 표시하려면 인스턴스 내에 광고 컨테이너( `AdContainerView`)를 제공해야 합니다 `MediaPlayerContext` .

VPAID 광고의 제한 사항:

* 광고가 대화형일 수 있으므로 VPAID 광고의 지속 시간이 사전 정의된 것은 아닙니다. 따라서 광고 서버 응답으로 정의된 광고 지속 시간이 광고의 실제 지속 시간과 항상 정확하게 일치하지는 않을 수 있습니다.
* VPAID 1.0 광고의 경우 TVSDK를 사용하려면 장치에 Flash player 14.0.0.160 이상이 설치되어 있어야 합니다. 이전 버전의 Flash Player에서는 이 기능이 비활성화되어 VPAID 1.0 광고를 건너뜁니다.

광고 브레이크 내에서 VPAID 광고(버전 1.0 또는 2.0)를 표시하기 위한 광고 컨테이너를 설정하려면

1. 다음 샘플 코드를 사용하여 VPAID 광고를 표시할 수 있는 광고 컨테이너를 설정합니다.

   ```
   var context:MediaPlayerContext =  
     new MediaPlayerContext(_authorizedFeatureHelper.authorizedFeatures); 
   
   adContainer = new AdContainerView(); 
   adContainer.x = adContainer.y = 0; 
   adContainer.setSize(videoContainer.width, videoContainer.height); 
   addChild(adContainer); 
   
   context.adContainer = adContainer; 
   _player = new DefaultMediaPlayer(context);
   ```

1. 보기 크기가 조정되면 광고 컨테이너의 크기를 재설정합니다.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >전체 화면 변경 이벤트를 받고 광고 컨테이너에 새 크기를 설정하면 플레이어 크기가 올바르게 조절되도록 다음과 같이 스테이지 표시 상태를 전달합니다.   >
   >
   >
   ```>
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```   >
   >



