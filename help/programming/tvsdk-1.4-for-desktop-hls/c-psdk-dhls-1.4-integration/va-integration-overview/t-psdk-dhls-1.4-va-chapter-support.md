---
description: 'null'
seo-description: 'null'
seo-title: 장 지원 구현
title: 장 지원 구현
uuid: 85d14b83-7910-4f5d-9ef2-511de916abd6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 장 지원 구현 {#implement-chapter-support}

다음과 같은 방법으로 TVSDK 기반 애플리케이션에서 비디오 추적을 위한 장을 정의하고 추적할 수 있습니다.

* TVSDK에서 내부적으로 관리하는 기본 장.

   장은 각 광고 중단 사이의 시간으로 정의됩니다. 예를 들어 프리롤 광고 브레이크와 첫 번째 미드롤 사이의 시간은 첫 번째 장으로 정의됩니다.
* 애플리케이션에서 관리되고 CMS 데이터 또는 애플리케이션에서 장(chapter)을 정의하는 데 사용하는 다른 방법을 기반으로 하는 맞춤형 장(chapter)

   기본 장 또는 사용자 정의 장을 정의하고 추적할 수 있습니다.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaMetadata.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example: 3 chapters of 60 second duration each 
   
       var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
       var chapterDuration:int = 60; 
       for (var i:int = 0; i < 3; i++) { 
           var chapterData:VideoAnalyticsChapterData =  
             new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
           chapterData.name = "chapter_%d" + (i+1); 
   
           chapters.push(chapterData); 
       } 
   
       vaMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above. 
   ```

