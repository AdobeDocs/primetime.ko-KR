---
description: 콜백 함수를 사용하여 콘텐츠, 광고 및 챕터 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.
title: 사용자 지정 메타데이터 지원 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 사용자 지정 메타데이터 지원 구현{#implement-custom-metadata-support}

콜백 함수를 사용하여 콘텐츠, 광고 및 챕터 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 바로 전에 호출되므로 응용 프로그램에서 광고 또는 챕터에 고유한 메타데이터를 첨부할 수 있습니다.

1. 콘텐츠, 광고 및 챕터에 대한 콜백 함수를 호출합니다.

   ```
   // Video Metadata Block 
   vaMetadata.videoMetadataBlock = function():Object { 
       return {"myvideoid":"1234", "mysdkversion":Version.version} 
   }; 
   
   // Ad Metadata Block invoked on every ad start 
   vaMetadata.adMetadataBlock = function(ad:Ad):Object { 
       return {"myadid":"ad-1234", "myad-sdkversion":Version.version} 
   }; 
   
   // Chapter Metadata Block invoked on every chapter start 
   vaMetadata.chapterMetadataBlock = function(chapter:VideoAnalyticsChapterData) { 
       return {"mychapterid":"chapter-1234", "mychapter-sdkversion":Version.version} 
   };
   ```
