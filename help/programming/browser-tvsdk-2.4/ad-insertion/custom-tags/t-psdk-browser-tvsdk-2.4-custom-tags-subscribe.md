---
description: 브라우저 TVSDK는 MPD(Media Presentation Description) 파일에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.
title: 사용자 정의 광고 태그 구독
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 사용자 지정 광고 태그 구독{#subscribe-to-custom-ad-tags}

브라우저 TVSDK는 MPD(Media Presentation Description) 파일에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.

재생이 시작되기 전에 태그에 가입해야 합니다.
태그에 가입하려면 사용자 지정 태그 이름이 포함된 벡터를 `subscribedTags` 속성으로 설정합니다. 기본 기회 생성기에서 사용되는 광고 태그도 변경해야 하는 경우 사용자 지정 광고 태그 이름이 포함된 벡터를 `adTags` 속성으로 설정합니다.

사용자 지정 태그를 구독하려면:

1. 새 미디어 플레이어 항목 구성을 만듭니다.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. 빈 문자열 벡터를 만듭니다.

   ```js
   var subscribeTags = [];
   ```

1. 이 벡터에 사용자 지정 태그 이름을 추가합니다.

   >[!IMPORTANT]
   >
   >HLS 스트림을 처리하는 경우 `#` 접두어를 포함해야 합니다.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 업데이트된 벡터를 `mediaPlayerItemConfig.subscribeTags` 속성에 할당합니다.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. 빈 문자열 벡터를 만듭니다.

   ```js
   var adTags= [];
   ```

1. 이 벡터에 사용자 지정 광고 태그 이름을 추가합니다.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. 업데이트된 벡터를 `mediaPlayerItemConfig.adTags` 속성에 할당합니다.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 미디어 스트림을 로드할 때 미디어 플레이어 항목 구성을 사용합니다.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

