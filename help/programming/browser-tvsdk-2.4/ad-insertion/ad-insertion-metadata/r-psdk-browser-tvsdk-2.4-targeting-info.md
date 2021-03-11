---
description: Adobe Primetime 광고 결정에서 키-값 쌍으로 광고를 타깃팅할 수 있습니다.
title: 타깃팅 정보
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# 타깃팅 정보{#targeting-information}

Adobe Primetime 광고 결정에서 키-값 쌍으로 광고를 타깃팅할 수 있습니다.

이러한 키 값 쌍을 브라우저 TVSDK로 전달하려면:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

