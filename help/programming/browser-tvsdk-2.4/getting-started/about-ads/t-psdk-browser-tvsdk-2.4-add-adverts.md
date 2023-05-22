---
title: 광고 추가
description: 광고 추가
copied-description: true
exl-id: 72f875ea-80ae-482b-94be-41116fff3614
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# 광고 추가 {#add-advertising}

1. 광고 메타데이터를 정의합니다.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. 에 광고 메타데이터 추가 `MediaResource`.

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. 구성에 설정을 추가하고 `SpliceOut` 구문 분석기 팩토리입니다.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. 추가 `ExtCueOutContentFactory` 라이브러리 섹션으로 이동합니다.
1. 다운로드 `ExtCueOutContentFactory.js` 라이브러리 섹션에서 가져온 다음 작업 폴더에 넣습니다.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. 구성을 테스트합니다.
