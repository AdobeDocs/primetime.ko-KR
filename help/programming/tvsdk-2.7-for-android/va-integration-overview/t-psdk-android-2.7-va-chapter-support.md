---
title: 장 지원 구현
description: 장 지원 구현
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# 장 지원 구현 {#implement-chapter-support}

TVSDK 기반 응용 프로그램에서 비디오 추적을 위해 *custom* 장을 정의하고 추적할 수 있습니다.

사용자 정의 장은 애플리케이션에서 관리되며, CMS 데이터 또는 애플리케이션에서 장 정의에 사용하는 다른 방법을 기반으로 합니다.

>[!CAUTION]
>
>2.5 Android TVSDK에서는 기본 장이 지원되지 않습니다.

1. 사용자 정의 장을 정의하고 추적할 수 있습니다.

   ```java
   // First, enable chapter tracking by setting   
   // enableChapterTracking to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide  
   // an array list of chapters through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters =  
     new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   ```

