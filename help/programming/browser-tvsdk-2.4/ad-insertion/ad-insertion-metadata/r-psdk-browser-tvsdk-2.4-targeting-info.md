---
description: Adobe Primetime 광고 결정에서는 키-값 쌍으로 광고를 타깃팅할 수 있습니다.
seo-description: Adobe Primetime 광고 결정에서는 키-값 쌍으로 광고를 타깃팅할 수 있습니다.
seo-title: 타깃팅 정보
title: 타깃팅 정보
uuid: 72114bef-36a1-4f2d-92e8-59f4885d70d2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 타깃팅 정보{#targeting-information}

Adobe Primetime 광고 결정에서는 키-값 쌍으로 광고를 타깃팅할 수 있습니다.

이러한 키 값 쌍을 브라우저 TVSDK로 전달하려면:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

