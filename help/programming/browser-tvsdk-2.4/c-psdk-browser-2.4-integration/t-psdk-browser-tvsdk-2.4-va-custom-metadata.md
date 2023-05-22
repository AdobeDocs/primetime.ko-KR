---
description: 콜백 함수를 사용하여 콘텐츠, 광고 및 챕터 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.
title: 사용자 지정 메타데이터 지원 구현
exl-id: d2291649-79e2-4935-8980-4f2038d58342
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 사용자 지정 메타데이터 지원 구현{#implement-custom-metadata-support}

콜백 함수를 사용하여 콘텐츠, 광고 및 챕터 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 바로 전에 호출되므로 응용 프로그램에서 광고 또는 챕터에 고유한 메타데이터를 첨부할 수 있습니다.

1. 콘텐츠, 광고 및 챕터에 대한 콜백 함수를 호출합니다.

   ```js
   vaObj.videoMetadataBlock = function() { 
       return { 
           "name" : "my-video", 
           "genre" : "comedy" 
       }; 
   } 
   
   vaObj.adMetadataBlock = function(ad) { 
       return { 
           "name" : "my-ad", 
           "category" : "automotive" 
       }; 
   } 
   
   vaObj.chapterMetadataBlock = function(chapter) { 
       return { 
           "name" : "my-chapter", 
           "type" : "quartile" 
       }; 
   }
   ```
