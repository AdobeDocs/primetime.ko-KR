---
description: 'null'
seo-description: 'null'
seo-title: 광고 추가
title: 광고 추가
uuid: 7762506f-b55e-445d-b8a2-c1208358a370
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# 광고 {#add-advertising} 추가

1. 광고 메타데이터를 정의합니다.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. 광고 메타데이터를 `MediaResource`에 추가합니다.

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. 구성에 설정을 추가하고 `SpliceOut` 파서 팩터리를 추가합니다.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. 라이브러리 섹션에 `ExtCueOutContentFactory`을(를) 추가합니다.
1. 라이브러리 섹션에서 `ExtCueOutContentFactory.js`을 다운로드하고 작업 폴더에 배치합니다.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. 구성을 테스트합니다.
