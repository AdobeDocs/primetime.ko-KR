---
description: TVSDK는 이러한 개체가 콘텐츠 매니페스트에서 발견될 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.
title: 사용자 정의 태그 구독
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# 사용자 정의 태그 {#subscribe-to-custom-tags} 구독

TVSDK는 이러한 개체가 콘텐츠 매니페스트에서 발견될 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.

재생이 시작되기 전에 태그에 가입해야 합니다.
HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

1. 사용자 지정 태그가 포함된 배열을 `PTSDKConfig`의 `setSubscribedTags`에 전달하여 사용자 지정 광고 태그 이름을 전체적으로 설정합니다.

   >[!IMPORTANT]
   >
   >HLS 스트림을 사용할 때는 `#` 접두어를 포함해야 합니다.

   예:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

