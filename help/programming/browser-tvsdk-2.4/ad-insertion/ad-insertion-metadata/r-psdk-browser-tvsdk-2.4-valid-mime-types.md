---
description: 광고에 여러 크리에이티브한 요소가 있을 수 있으며 이 중 하나를 재생하도록 선택할 수 있습니다.
title: 유효한 MIME 유형
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# 유효한 MIME 유형{#valid-mime-types}

광고에 여러 크리에이티브한 요소가 있을 수 있으며 이 중 하나를 재생하도록 선택할 수 있습니다.

MIME 유형을 사용하여 사용자가 우선 순위를 정할 수 있는 크리에이티브 유형을 지정할 수 있습니다. 사용자가 지정하는 MIME 유형과 Browser TVSDK에서 지원하는 MIME 형식을 사용하여 우선 순위를 지정할 크리에이티브 유형을 결정합니다.

브라우저 TVSDK에서 유효한 MIME 유형을 설정하려면:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

여기서 `mimeTypes`은 문자열 배열이고 각 문자열은 mime 유형을 나타냅니다.

광고에 대해 여러 미디어 파일이 반환되는 경우 선택 사항은 미디어 파일이 `validMimeTypes` 배열에 나타나는 순서에 따라 달라집니다. 색인이 낮은 MIME 형식은 인덱스가 높은 MIME 유형보다 선호도가 높습니다.
