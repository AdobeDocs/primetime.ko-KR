---
description: 콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-description: 콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-title: 사용자 정의 메타데이터 지원 구현
title: 사용자 정의 메타데이터 지원 구현
uuid: 6e23311c-a393-4485-919e-4cf6412789b1
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 사용자 정의 메타데이터 지원 구현{#implement-custom-metadata-support}

콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 직전에 호출되므로 애플리케이션에서 광고 또는 장에 해당하는 메타데이터를 첨부할 수 있습니다.

1. 콘텐츠, 광고 및 장에 대한 콜백 함수를 호출합니다.

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

