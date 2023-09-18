---
description: 소스 목록의 forceflash 플래그는 URL에 대한 Flash 폴백을 강제 적용합니다. 이 URL의 경우 Adobe Flash Player을 사용하여 콘텐츠를 재생할 수 있습니다.
title: 미디어 소스 목록을 사용하여 Flash 폴백 강제 실행
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 미디어 소스 목록을 사용하여 Flash 폴백 강제 실행{#forcing-the-flash-fallback-using-the-media-source-list}

소스 목록의 forceflash 플래그는 URL에 대한 Flash 폴백을 강제 적용합니다. 이 URL의 경우 Adobe Flash Player을 사용하여 콘텐츠를 재생할 수 있습니다.

미디어 소스 목록(예: `sources.js` file), 다음을 설정할 수 있습니다. `forceflash` 끝 `true`. 예:

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
