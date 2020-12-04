---
description: TVSDK는 이러한 개체가 컨텐츠 매니페스트에서 나타날 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.
seo-description: TVSDK는 이러한 개체가 컨텐츠 매니페스트에서 나타날 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.
seo-title: 사용자 정의 태그 구독
title: 사용자 정의 태그 구독
uuid: e47076b2-6184-4c20-bae4-ba7ae62cf198
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---


# 사용자 지정 태그 {#subscribe-to-custom-tags} 구독

TVSDK는 이러한 개체가 컨텐츠 매니페스트에서 나타날 때마다 구독 태그의 PTTimedMetadata 개체를 준비합니다.

재생을 시작하기 전에 태그에 가입해야 합니다.
HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

1. 사용자 지정 태그가 포함된 배열을 `PTSDKConfig`의 `setSubscribedTags`으로 전달하여 사용자 지정 광고 태그 이름을 전역적으로 설정합니다.

   >[!IMPORTANT]
   >
   >HLS 스트림을 사용하여 작업할 때는 `#` 접두어를 포함해야 합니다.

   예:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
