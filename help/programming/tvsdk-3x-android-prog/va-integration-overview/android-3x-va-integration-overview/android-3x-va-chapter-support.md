---
title: 챕터 지원 구현
description: 챕터 지원 구현
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# 챕터 지원 구현 {#implement-chapter-support}

을 정의하고 추적할 수 있습니다 *사용자 정의* tvsdk 기반 애플리케이션에서 비디오 추적을 위한 챕터입니다.

사용자 정의 챕터는 애플리케이션에서 관리되며 CMS 데이터 또는 애플리케이션에서 챕터를 정의하는 데 사용하는 다른 방법에 따라 결정됩니다.

>[!CAUTION]
>
>3.0 Android TVSDK에서는 기본 챕터가 지원되지 않습니다.

사용자 지정 챕터를 정의하고 추적합니다.

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
