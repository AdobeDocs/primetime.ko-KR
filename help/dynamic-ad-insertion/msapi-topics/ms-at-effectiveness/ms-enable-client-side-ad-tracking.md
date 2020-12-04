---
description: Bootstrap URL 요청에 pttrackingmode 및 pttrackingversion 매개 변수를 추가하여 클라이언트측 광고 추적을 활성화할 수 있습니다.
seo-description: Bootstrap URL 요청에 pttrackingmode 및 pttrackingversion 매개 변수를 추가하여 클라이언트측 광고 추적을 활성화할 수 있습니다.
seo-title: 클라이언트측 광고 추적 활성화
title: 클라이언트측 광고 추적 활성화
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 클라이언트측 광고 추적 활성화 {#enable-client-side-ad-tracking}

Bootstrap URL 요청에 `pttrackingmode` 및 `pttrackingversion` 매개 변수를 추가하여 클라이언트측 광고 추적을 활성화할 수 있습니다.

클라이언트측 광고 추적이 활성화되면 추적 API URL을 사용하여 광고 추적 메타데이터를 검색할 수도 있습니다. 자세한 내용은 [쿼리 매개 변수](../../msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)를 참조하십시오.

클라이언트측 광고 추적을 수행하려면 추적 API URL을 사용합니다.

1. 매니페스트 서버 요청 URL에 다음 쿼리 매개 변수를 추가합니다.

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

예:

```
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
