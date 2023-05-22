---
description: Adobe Primetime 광고 의사 결정에서 키-값 쌍에 광고를 타깃팅할 수 있습니다.
title: 타겟팅 정보
exl-id: 25610f7d-6b14-4ed1-b61c-9e6bf13ba8e6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
