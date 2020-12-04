---
description: 'null'
seo-description: 'null'
seo-title: 장 지원 구현
title: 장 지원 구현
uuid: 70f10621-febe-4443-84e7-ce95bec53377
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# 장 지원 구현{#implement-chapter-support}

장은 각 광고 중단 사이의 시간으로 정의됩니다. 예를 들어 프리롤 광고 중단과 첫 번째 중간 롤의 시간 사이의 시간은 첫 번째 장으로 정의됩니다. 사용자 정의 장을 사용하여 브라우저 TVSDK 기반 애플리케이션에서 비디오 추적을 위한 장을 정의하고 추적할 수 있습니다. 사용자 지정 장은 애플리케이션에서 관리되며 CMS 데이터 또는 응용 프로그램이 장 정의에 사용하는 다른 방법을 기반으로 합니다.

1. 맞춤형 장 정의 및 추적

   ```js
   vaObj.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
   
   vaObj.chapters = chapters;
   ```

