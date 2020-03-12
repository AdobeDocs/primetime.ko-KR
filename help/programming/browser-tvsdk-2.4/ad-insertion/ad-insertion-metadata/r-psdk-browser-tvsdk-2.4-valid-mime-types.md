---
description: 광고에 여러 크리에이티브가 있을 수 있으며 이 중 하나를 선택하여 재생할 수 있습니다.
seo-description: 광고에 여러 크리에이티브가 있을 수 있으며 이 중 하나를 선택하여 재생할 수 있습니다.
seo-title: 유효한 MIME 유형
title: 유효한 MIME 유형
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 유효한 MIME 유형{#valid-mime-types}

광고에 여러 크리에이티브가 있을 수 있으며 이 중 하나를 선택하여 재생할 수 있습니다.

MIME 유형을 사용하여 사용자가 우선 순위를 지정할 수 있는 크리에이티브 유형을 지정할 수 있습니다. 사용자가 지정한 MIME 유형과 Browser TVSDK에서 지원하는 MIME 유형을 사용하여 우선 순위를 지정할 크리에이티브 유형을 결정합니다.

Browser TVSDK에서 유효한 MIME 유형을 설정하려면

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

여기서 `mimeTypes` 는 문자열 배열이고 각 문자열은 mime 형식을 나타냅니다.

광고에 대해 여러 미디어 파일이 반환되는 경우 선택 사항은 미디어 파일이 `validMimeTypes` 배열에 표시되는 순서에 따라 달라집니다. 인덱스가 낮은 MIME 형식에는 인덱스가 더 높은 MIME 유형보다 선호도가 지정됩니다.
