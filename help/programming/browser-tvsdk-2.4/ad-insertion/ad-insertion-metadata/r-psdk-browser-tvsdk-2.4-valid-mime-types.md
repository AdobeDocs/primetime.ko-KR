---
description: 광고에는 여러 개의 크리에이티브가 있을 수 있으며 그중 하나는 재생되도록 선택됩니다.
title: 유효한 MIME 유형
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 유효한 MIME 유형{#valid-mime-types}

광고에는 여러 개의 크리에이티브가 있을 수 있으며 그중 하나는 재생되도록 선택됩니다.

MIME 유형을 사용하면 우선 순위를 지정할 수 있는 크리에이티브 유형 사용자를 지정할 수 있습니다. 사용자가 지정한 MIME 유형과 브라우저 TVSDK에서 지원하는 MIME 유형을 사용하여 우선 순위가 지정될 크리에이티브를 결정합니다.

브라우저 TVSDK에서 올바른 MIME 유형을 설정하려면 다음을 수행하십시오.

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

위치 `mimeTypes` 는 문자열의 배열이며 각 문자열은 mime 유형을 나타냅니다.

광고에 대해 여러 미디어 파일이 반환되는 경우, 선택 사항은 미디어 파일이 표시되는 순서에 따라 다릅니다 `validMimeTypes` 배열입니다. 색인이 낮은 MIME 유형은 색인이 높은 MIME보다 우선 순위가 높습니다.
