---
description: 광고에 여러 개의 크리에이티브가 있는데, 그 중 하나를 재생하도록 선택할 수 있습니다.
seo-description: 광고에 여러 개의 크리에이티브가 있는데, 그 중 하나를 재생하도록 선택할 수 있습니다.
seo-title: 유효한 MIME 형식
title: 유효한 MIME 형식
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 유효한 MIME 유형{#valid-mime-types}

광고에 여러 개의 크리에이티브가 있는데, 그 중 하나를 재생하도록 선택할 수 있습니다.

MIME 유형을 사용하여 사용자가 우선 순위를 정할 수 있는 크리에이티브 유형을 지정할 수 있습니다. 사용자가 지정하는 MIME 형식과 Browser TVSDK에서 지원하는 MIME 유형은 우선 순위를 정할 때 사용됩니다.

Browser TVSDK에서 유효한 MIME 유형을 설정하려면:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

여기서 `mimeTypes`은 문자열 배열이고 각 문자열은 mime 형식을 나타냅니다.

광고에 대해 여러 미디어 파일이 반환되는 경우 선택 사항은 미디어 파일이 `validMimeTypes` 배열에 나타나는 순서에 따라 달라집니다. 색인이 낮은 MIME 형식은 인덱스가 더 높은 MIME 유형보다 선호됩니다.
