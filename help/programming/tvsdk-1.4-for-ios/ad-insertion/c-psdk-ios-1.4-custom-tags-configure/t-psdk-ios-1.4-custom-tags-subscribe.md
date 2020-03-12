---
description: TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 발견될 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.
seo-description: TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 발견될 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.
seo-title: 사용자 정의 태그 구독
title: 사용자 정의 태그 구독
uuid: de66d3db-46d1-485f-9d3a-6e28495bfb13
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 정의 태그 구독 {#subscribe-to-custom-tags}

TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 발견될 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.

재생이 시작되기 전에 태그에 가입해야 합니다.
HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

1. 사용자 지정 태그가 포함된 배열을 전달하여 사용자 지정 광고 태그 이름을 전체적으로 `setSubscribedTags` 설정합니다 `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >HLS 스트림을 사용하여 작업할 때는 `#` 접두사를 포함해야 합니다.

   예:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

