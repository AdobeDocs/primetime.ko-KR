---
title: 챕터 지원 구현
description: 챕터 지원 구현
copied-description: true
exl-id: 4585505c-9511-4f10-b81a-922eaeb2764d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 챕터 지원 구현{#implement-chapter-support}

다음과 같은 방법으로 TVSDK 기반 애플리케이션에서 비디오 추적을 위한 챕터를 정의하고 추적할 수 있습니다.

* TVSDK에 의해 내부적으로 관리되는 기본 챕터입니다.

   챕터는 각 광고 브레이크 사이의 시간으로 정의됩니다. 예를 들어 프리롤 광고 브레이크와 첫 번째 미드롤 사이의 시간을 첫 번째 챕터로 정의합니다.
* 응용 프로그램에서 관리하며 CMS 데이터 또는 응용 프로그램에서 챕터를 정의하는 데 사용하는 다른 방법을 기반으로 하는 사용자 지정 챕터입니다.

   기본 또는 사용자 지정 챕터를 정의하고 추적합니다.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaTrackingMetadata.enableChapterTracking = YES; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example, 3 chapters of 60 second duration each: 
   
       NSMutableArray *chapters = [[[NSMutableArray alloc] init] autorelease]; 
   
       int chapterDuration = 60; 
       for (int i = 0; i < 3; i++) 
       { 
           PTVideoAnalyticsChapterData *chapterData =  
             [[[PTVideoAnalyticsChapterData alloc] init] autorelease]; 
           chapterData.name = [NSString stringWithFormat:@"chapter_%d", (i+1)]; 
           chapterData.range =  
             CMTimeRangeMake(CMTimeMakeWithSeconds(i * chapterDuration, 10000),  
             CMTimeMakeWithSeconds(chapterDuration, 10000)); 
   
           [chapters addObject:chapterData]; 
       } 
   
       vaTrackingMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above.
   ```
