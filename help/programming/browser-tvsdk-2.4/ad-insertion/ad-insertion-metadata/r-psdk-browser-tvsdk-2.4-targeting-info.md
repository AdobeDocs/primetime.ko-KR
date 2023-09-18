---
description: Adobe Primetime 광고 의사 결정에서 키-값 쌍에 광고를 타깃팅할 수 있습니다.
title: 타겟팅 정보
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 타겟팅 정보{#targeting-information}

Adobe Primetime 광고 의사 결정에서 키-값 쌍에 광고를 타깃팅할 수 있습니다.

이러한 키 값 쌍을 브라우저 TVSDK에 전달하려면:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
