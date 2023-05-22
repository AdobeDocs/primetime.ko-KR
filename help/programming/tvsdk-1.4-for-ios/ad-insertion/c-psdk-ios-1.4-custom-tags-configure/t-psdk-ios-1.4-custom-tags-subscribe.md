---
description: TVSDK는 콘텐츠 매니페스트에서 해당 개체가 발견될 때마다 구독한 태그에 대한 PTTimedMetadata 개체를 준비합니다.
title: 사용자 정의 태그 구독
exl-id: 85d13ae1-d33c-4394-b9fa-a66024974c8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 사용자 정의 태그 구독 {#subscribe-to-custom-tags}

TVSDK는 콘텐츠 매니페스트에서 해당 개체가 발견될 때마다 구독한 태그에 대한 PTTimedMetadata 개체를 준비합니다.

재생이 시작되기 전에 태그를 구독해야 합니다.
HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

1. 사용자 지정 태그가 포함된 배열을 로 전달하여 사용자 지정 광고 태그 이름을 전체적으로 설정합니다. `setSubscribedTags` 위치: `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >다음을 포함해야 합니다. `#` hls 스트림 작업 시 접두사를 사용합니다.

   예:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
