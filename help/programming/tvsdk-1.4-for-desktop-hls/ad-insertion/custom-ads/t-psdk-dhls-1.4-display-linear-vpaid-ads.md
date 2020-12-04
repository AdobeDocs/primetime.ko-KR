---
description: TVSDK는 광고 중단에서 선형 비디오 플레이어-광고 인터페이스 정의(VPAID) 광고 표시를 지원합니다. VPAID 버전 1.0에는 Flash이 필요하며 버전 2.0은 Browser TVSDK 및 JavaScript에서도 작동합니다.
seo-description: TVSDK는 광고 중단에서 선형 비디오 플레이어-광고 인터페이스 정의(VPAID) 광고 표시를 지원합니다. VPAID 버전 1.0에는 Flash이 필요하며 버전 2.0은 Browser TVSDK 및 JavaScript에서도 작동합니다.
seo-title: 선형 VPAID 광고를 광고 중단으로 표시
title: 선형 VPAID 광고를 광고 중단으로 표시
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 선형 VPAID 광고를 광고 중단{#display-linear-vpaid-ads-in-an-ad-break}에 표시

TVSDK는 광고 중단에서 선형 비디오 플레이어-광고 인터페이스 정의(VPAID) 광고 표시를 지원합니다. VPAID 버전 1.0에는 Flash이 필요하며 버전 2.0은 Browser TVSDK 및 JavaScript에서도 작동합니다.

VPAID 광고를 올바르게 표시하려면 `MediaPlayerContext` 인스턴스 내에 광고 컨테이너( `AdContainerView`)를 제공해야 합니다.

VPAID 광고의 제한 사항:

* 광고가 대화형일 수 있기 때문에 VPAID 광고에 사전 정의된 기간이 반드시 있는 것은 아닙니다. 따라서 광고 서버 응답으로 정의된 광고 지속 시간이 광고의 실제 지속 시간과 항상 정확하게 일치하지 않을 수 있습니다.
* VPAID 1.0 광고의 경우 TVSDK에는 장치에 Flash 플레이어 14.0.0.160 이상이 설치되어 있어야 합니다. 이전 버전의 Flash 플레이어의 경우 이 기능이 비활성화되어 VPAID 1.0 광고를 건너뜁니다.

광고 중단 내에 VPAID 광고(버전 1.0 또는 2.0)를 표시하기 위한 광고 컨테이너를 설정하려면 다음을 수행하십시오.

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
   >전체 화면 변경 이벤트를 받고 광고 컨테이너에 새 크기를 설정하면 플레이어 크기가 올바르게 조절되도록 다음과 같이 스테이지 표시 상태를 전달합니다.
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

