---
description: 'null'
seo-description: 'null'
seo-title: 장 지원 구현
title: 장 지원 구현
uuid: 5b39e494-85ad-43bb-ab56-a55797aa4ef7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 장 지원 구현 {#implement-chapter-support}

다음 방법으로 TVSDK 기반 응용 프로그램에서 비디오 추적을 위한 장을 정의하고 추적할 수 있습니다.

* TVSDK에서 내부적으로 관리하는 기본 장.

   장은 각 광고 중단 사이의 시간으로 정의됩니다. 예를 들어 프리롤 광고 중단과 첫 번째 중간 롤의 시간 사이의 시간은 첫 번째 장으로 정의됩니다.
* 애플리케이션에서 관리되고 CMS 데이터 또는 응용 프로그램이 장 정의에 사용하는 다른 방법을 기반으로 하는 사용자 정의 장(chapter)입니다.

1. 기본 장 또는 사용자 정의 장을 정의하고 추적할 수 있습니다.

   ```java
   // First, enable chapter tracking by setting  
   // the Boolean 'enableChapterTracking' to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide an array list of chapters  
   // through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters = new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   // For default chapters, the application must not set  
   // custom chapters on the tracking metadata 
   // and simply enable chapters to be tracked by setting  
   // the boolean value as defined above.
   ```
