---
description: TVSDK는 콘텐츠 매니페스트에서 태그가 발견될 때마다 구독한 태그에 대한 TimedMetadata 개체를 준비합니다.
title: 사용자 정의 태그 구독
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 사용자 정의 태그 구독{#subscribe-to-custom-tags}

TVSDK는 콘텐츠 매니페스트에서 태그가 발견될 때마다 구독한 태그에 대한 TimedMetadata 개체를 준비합니다.

재생이 시작되기 전에 태그를 구독해야 합니다.
태그를 구독하려면 사용자 지정 태그 이름이 포함된 벡터를 `subscribedTags` 속성. 기본 영업 기회 생성기에서 사용하는 광고 태그도 변경해야 하는 경우 사용자 지정 광고 태그 이름이 포함된 벡터를 `adTags` 속성.

HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

1. 사용자 지정 태그가 포함된 벡터를 할당하여 사용자 지정 광고 태그 이름을 전체적으로 설정합니다. `subscribeTags` 위치: `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >다음을 포함해야 합니다. `#` hls 스트림 작업 시 접두사를 사용합니다.

   예:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 기본 영업 기회 생성기에서 사용하는 광고 태그를 전역적으로 변경하려면 사용자 지정 광고 태그 이름이 포함된 벡터를 `adTags` 의 속성 `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 모든 전역 설정을 적용하려면 현재 리소스를 바꿉니다.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 필요한 경우 스트림에 대해 구독한 태그 이름을 설정하려면 다음을 수행하십시오.
   1. 미디어 플레이어 항목 구성을 만듭니다.

      >[!TIP]
      >
      >가장 쉬운 방법은 기본 미디어 플레이어 항목 구성을 만드는 것입니다.

   1. 사용자 지정 태그가 포함된 벡터 할당 `subscribeTags` 위치: `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 지정된 스트림에서 기본 영업 기회 생성기에 사용되는 광고 태그를 변경하려면 사용자 지정 광고 태그 이름이 포함된 벡터를 `adTags` 의 속성 `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 미디어 스트림을 로드할 때 스트림에 대한 변경 사항을 적용하려면 미디어 플레이어 항목 구성을 사용하십시오.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
