---
description: 콜백 함수를 사용하여 콘텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-description: 콜백 함수를 사용하여 콘텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.
seo-title: 사용자 정의 메타데이터 지원 구현
title: 사용자 정의 메타데이터 지원 구현
uuid: 229681f5-ff77-4321-8022-b8ccf2928fb3
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# 사용자 지정 메타데이터 지원 구현 {#implement-custom-metadata-support}

콜백 함수를 사용하여 콘텐츠, 광고 및 장 추적 호출에 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 직전에 호출되므로 응용 프로그램에서 광고 또는 장에 해당하는 메타데이터를 첨부할 수 있습니다.

1. 콘텐츠, 광고 및 장에 대한 콜백 함수를 호출합니다.

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
