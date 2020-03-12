---
description: 콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-description: 콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-title: 사용자 정의 메타데이터 지원 구현
title: 사용자 정의 메타데이터 지원 구현
uuid: 2186db58-10b0-43a6-840f-53ab289843ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 사용자 정의 메타데이터 지원 구현{#implement-custom-metadata-support}

콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 직전에 호출되므로 애플리케이션에서 광고 또는 장에 해당하는 메타데이터를 첨부할 수 있습니다.

1. 콘텐츠, 광고 및 장에 대한 콜백 함수를 호출합니다.

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

