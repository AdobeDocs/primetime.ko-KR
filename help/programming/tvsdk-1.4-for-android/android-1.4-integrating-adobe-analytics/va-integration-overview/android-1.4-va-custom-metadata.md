---
description: 콜백 함수를 사용하여 콘텐츠, 광고 및 챕터 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.
title: 사용자 지정 메타데이터 지원 구현
exl-id: 59d56d5e-959d-4fb3-8434-55ae8219fca6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# 사용자 지정 메타데이터 지원 구현 {#implement-custom-metadata-support}

콜백 함수를 사용하여 콘텐츠, 광고 및 챕터 추적 호출에 대한 사용자 지정 메타데이터를 제공할 수 있습니다.

콜백 함수는 추적 호출이 수행되기 바로 전에 호출되므로 응용 프로그램에서 광고 또는 챕터에 고유한 메타데이터를 첨부할 수 있습니다.

콘텐츠, 광고 및 챕터에 대한 콜백 함수를 호출합니다.

```java
// Video Metadata Block 
vaMetadata.setVideoMetadataBlock(new VideoAnalyticsMetadata.VideoMetadataBlock() { 
    @Override 
    public HashMap<String, String> call() { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myvideoid", "1234"); 
        result.put("mysdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Ad Metadata Block invoked on every ad start 
vaMetadata.setAdMetadataBlock(new VideoAnalyticsMetadata.AdMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(Ad ad) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myadid", "ad-1234"); 
        result.put("myad-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Chapter Metadata Block invoked on every chapter start 
vaMetadata.setChapterMetadataBlock(new VideoAnalyticsMetadata.ChapterMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(VideoAnalyticsChapterData chapter) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("mychapterid", "chapter-1234"); 
        result.put("mychapter-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
});
```
