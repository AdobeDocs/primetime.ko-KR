---
title: 챕터 지원 구현
description: 챕터 지원 구현
copied-description: true
exl-id: 2db335b3-1d9b-4339-b1b6-e12ee0f06566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
