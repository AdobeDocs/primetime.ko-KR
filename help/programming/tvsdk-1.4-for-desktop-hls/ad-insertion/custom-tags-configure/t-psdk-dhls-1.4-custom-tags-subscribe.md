---
description: TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.
seo-description: TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.
seo-title: 사용자 정의 태그 구독
title: 사용자 정의 태그 구독
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 사용자 지정 태그 구독{#subscribe-to-custom-tags}

TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.

재생을 시작하기 전에 태그에 가입해야 합니다.
태그에 가입하려면 사용자 지정 태그 이름이 포함된 벡터를 `subscribedTags` 속성에 할당합니다. 기본 기회 생성기에서 사용하는 광고 태그도 변경해야 하는 경우 사용자 지정 광고 태그 이름이 포함된 벡터를 `adTags` 속성에 할당합니다.

HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

1. 사용자 지정 태그가 포함된 벡터를 `MediaPlayerItemConfig`의 `subscribeTags`에 할당하여 사용자 지정 광고 태그 이름을 전역적으로 설정합니다.

   >[!IMPORTANT]
   >
   >HLS 스트림을 사용하여 작업할 때는 `#` 접두어를 포함해야 합니다.

   예:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 기본 기회 생성기에서 사용하는 광고 태그를 전체적으로 변경하려면 사용자 지정 광고 태그 이름이 포함된 벡터를 `PSDKConfig`의 `adTags` 속성에 할당합니다.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 모든 전역 설정을 적용하려면 현재 리소스를 바꾸십시오.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 필요한 경우 스트림에 대해 구독된 태그 이름을 설정하려면:
   1. 미디어 플레이어 항목 구성을 만듭니다.

      >[!TIP]
      >
      >가장 쉬운 방법은 기본 미디어 플레이어 항목 구성을 만드는 것입니다.

   1. 사용자 지정 태그가 포함된 벡터를 `MediaPlayerItemConfig`의 `subscribeTags`에 할당합니다.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 지정된 스트림의 기본 기회 생성기에서 사용되는 광고 태그를 변경하려면 사용자 지정 광고 태그 이름을 포함하는 벡터를 `mediaPlayerItemConfig`의 `adTags` 속성에 할당합니다

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 스트림 변경 사항을 적용하려면 미디어 스트림을 로드할 때 미디어 플레이어 항목 구성을 사용하십시오.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

