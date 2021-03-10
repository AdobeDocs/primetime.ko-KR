---
description: TVSDK는 광고 노출에 선형 VPAID(Video Player-Ad Interface Definition) 광고를 표시할 수 있도록 지원합니다. VPAID 버전 1.0에는 Flash이 필요하며 버전 2.0은 브라우저 TVSDK 및 JavaScript에서도 작동합니다.
title: 광고 노출에 선형 VPAID 광고 표시
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 선형 VPAID 광고를 광고 중단{#display-linear-vpaid-ads-in-an-ad-break}에 표시

TVSDK는 광고 노출에 선형 VPAID(Video Player-Ad Interface Definition) 광고를 표시할 수 있도록 지원합니다. VPAID 버전 1.0에는 Flash이 필요하며 버전 2.0은 브라우저 TVSDK 및 JavaScript에서도 작동합니다.

VPAID 광고를 올바로 표시하려면 `MediaPlayerContext` 인스턴스 내에 광고 컨테이너( `AdContainerView`)를 제공해야 합니다.

VPAID 광고의 제한 사항:

* 광고가 대화형일 수 있기 때문에 VPAID 광고의 지속 시간이 사전 정의된 것은 아닙니다. 따라서 광고 서버 응답으로 정의된 광고 지속 시간이 광고의 실제 지속 시간과 항상 정확하게 일치하지 않을 수 있습니다.
* VPAID 1.0 광고의 경우 TVSDK에 Flash 플레이어 14.0.0.160 이상이 설치되어 있어야 합니다. 이전 버전의 Flash 플레이어의 경우 이 기능이 비활성화되고 VPAID 1.0 광고를 건너뜁니다.

광고 브레이크 내에서 VPAID 광고(버전 1.0 또는 2.0)를 표시하기 위한 광고 컨테이너를 설정하려면:

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
   >전체 화면 변경 이벤트를 수신하고 광고 컨테이너에 새 크기를 설정할 때 다음과 같이 스테이지 표시 상태를 전달하여 플레이어의 크기가 올바르게 조정되는지 확인합니다.
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

