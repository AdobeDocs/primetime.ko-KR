---
description: 소스 목록의 forceflash 플래그는 URL에 대한 Flash 폴백을 적용합니다. 이 URL의 경우 Adobe Flash Player을 사용하여 콘텐트를 재생할 수 있습니다.
seo-description: 소스 목록의 forceflash 플래그는 URL에 대한 Flash 폴백을 적용합니다. 이 URL의 경우 Adobe Flash Player을 사용하여 콘텐트를 재생할 수 있습니다.
seo-title: 미디어 소스 목록을 사용하여 Flash 폴백 강제 수행
title: 미디어 소스 목록을 사용하여 Flash 폴백 강제 수행
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 미디어 소스 목록{#forcing-the-flash-fallback-using-the-media-source-list}을(를) 사용하여 Flash 폴백 강제 수행

소스 목록의 forceflash 플래그는 URL에 대한 Flash 폴백을 적용합니다. 이 URL의 경우 Adobe Flash Player을 사용하여 콘텐트를 재생할 수 있습니다.

미디어 소스 목록(예: `sources.js` 파일)에서 `forceflash`을 `true`로 설정할 수 있습니다. 예:

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```

