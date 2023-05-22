---
description: TVSDK는 광고 브레이크에서 선형 비디오 플레이어 광고 인터페이스 정의(VPAID) 광고 표시를 지원합니다. VPAID 버전 1.0에는 Flash이 필요하지만, 버전 2.0은 브라우저 TVSDK 및 JavaScript에서도 작동합니다.
title: 광고 브레이크에 선형 VPAID 광고 표시
exl-id: 316a38ac-ec2d-498c-b441-304e2fa75993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 광고 브레이크에 선형 VPAID 광고 표시{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK는 광고 브레이크에서 선형 비디오 플레이어 광고 인터페이스 정의(VPAID) 광고 표시를 지원합니다. VPAID 버전 1.0에는 Flash이 필요하지만, 버전 2.0은 브라우저 TVSDK 및 JavaScript에서도 작동합니다.

VPAID 광고를 올바르게 표시하려면 광고 컨테이너( `AdContainerView`) 내의 `MediaPlayerContext` 인스턴스.

VPAID 광고 제한 사항:

* 광고가 대화형일 수 있다는 점에서 VPAID 광고에는 반드시 사전 정의된 기간이 있는 것은 아닙니다. 따라서 광고 기간(광고 서버 응답으로 정의됨)이 항상 광고의 실제 기간과 정확히 일치하는 것은 아닐 수 있습니다.
* VPAID 1.0 광고의 경우 TVSDK를 사용하려면 Flash 플레이어 14.0.0.160 이상이 장치에 설치되어 있어야 합니다. 이전 버전의 Flash 플레이어의 경우 이 기능이 비활성화되고 VPAID 1.0 광고를 건너뜁니다.

광고 브레이크 내에 VPAID 광고(버전 1.0 또는 2.0)를 표시하기 위한 광고 컨테이너를 설정하려면 다음을 수행하십시오.

1. 다음 샘플 코드를 사용하여 VPAID 광고를 표시할 수 있는 광고 컨테이너를 설정하십시오.

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

1. 보기 크기가 조정되면 광고 컨테이너에서 크기를 재설정합니다.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >전체 화면 변경 이벤트가 발생하고 광고 컨테이너에서 새 크기를 설정하면 단계 표시 상태를 다음과 같이 전달하여 플레이어의 크기가 올바르게 조정되도록 합니다.
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```
