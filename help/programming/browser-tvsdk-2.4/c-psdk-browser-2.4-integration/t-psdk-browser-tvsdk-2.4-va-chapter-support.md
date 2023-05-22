---
title: 챕터 지원 구현
description: 챕터 지원 구현
copied-description: true
exl-id: 8a962706-50cd-41c2-96a7-6af1b24145a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# 챕터 지원 구현{#implement-chapter-support}

챕터는 각 광고 브레이크 사이의 시간으로 정의됩니다. 예를 들어 프리롤 광고 브레이크와 첫 번째 미드롤 사이의 시간을 첫 번째 챕터로 정의합니다. 사용자 지정 챕터를 사용하여 브라우저 TVSDK 기반 애플리케이션에서 비디오 추적을 위한 챕터를 정의하고 추적할 수 있습니다. 사용자 정의 챕터는 애플리케이션에서 관리되며 CMS 데이터 또는 애플리케이션에서 챕터를 정의하는 데 사용하는 다른 방법을 기반으로 합니다.

1. 사용자 지정 챕터를 정의하고 추적합니다.

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
