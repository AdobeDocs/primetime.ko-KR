---
description: 콜백 함수를 사용하여 콘텐츠, 광고 및 장 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.
title: 사용자 정의 메타데이터 지원 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# 사용자 지정 메타데이터 지원 구현{#implement-custom-metadata-support}

콜백 함수를 사용하여 콘텐츠, 광고 및 장 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 직전에 호출되므로 응용 프로그램에서 광고 또는 장에 해당하는 메타데이터를 첨부할 수 있습니다.

1. 컨텐츠, 광고 및 장에 대한 콜백 함수를 호출합니다.

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

