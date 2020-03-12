---
description: 콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-description: 콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-title: 사용자 정의 메타데이터 지원 구현
title: 사용자 정의 메타데이터 지원 구현
uuid: eb8d383f-a3e8-402d-84e8-f4209df0f954
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 정의 메타데이터 지원 구현{#implement-custom-metadata-support}

콜백 함수를 사용하여 컨텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 직전에 호출되므로 애플리케이션에서 광고 또는 장에 해당하는 메타데이터를 첨부할 수 있습니다.

콘텐츠, 광고 및 장에 대한 콜백 함수를 호출합니다.

```
// Video Metadata Block 
    vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
    { 
        return @{ 
                 @"myvideoid": @"1234", 
                 @"mysdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Ad Metadata Block invoked on every ad start 
    vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
    { 
        return @{ 
                 @"myadid": @"ad-1234", 
                 @"myad-sdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Chapter Metadata Block invoked on every chapter start 
    vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
    { 
        return @{ 
                 @"mychapterid": @"chapter-1234", 
                 @"mychapter-sdkversion": [PTSDK apiVersion] 
                 }; 
    };
```

