---
description: 브라우저 TVSDK는 MPD(미디어 프레젠테이션 설명) 파일에서 이러한 개체가 발견될 때마다 구독한 태그에 대한 TimedMetadata 개체를 준비합니다.
title: 사용자 지정 광고 태그 구독
exl-id: d4b9ec3a-9c3f-4adf-984e-b45862e97140
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 사용자 지정 광고 태그 구독{#subscribe-to-custom-ad-tags}

브라우저 TVSDK는 MPD(미디어 프레젠테이션 설명) 파일에서 이러한 개체가 발견될 때마다 구독한 태그에 대한 TimedMetadata 개체를 준비합니다.

재생이 시작되기 전에 태그를 구독해야 합니다.
태그를 구독하려면 사용자 지정 태그 이름이 포함된 벡터를 `subscribedTags` 속성. 기본 영업 기회 생성기에서 사용하는 광고 태그를 변경해야 하는 경우 사용자 지정 광고 태그 이름이 포함된 벡터를 로 설정합니다. `adTags` 속성.

사용자 지정 태그에 가입하려면 다음을 수행하십시오.

1. 새 미디어 플레이어 항목 구성을 만듭니다.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. 빈 문자열 벡터를 만듭니다.

   ```js
   var subscribeTags = [];
   ```

1. 사용자 지정 태그 이름을 이 벡터에 추가합니다.

   >[!IMPORTANT]
   >
   >HLS 스트림을 처리하는 경우 다음을 포함해야 합니다. `#` 접두사입니다.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 업데이트된 벡터를 `mediaPlayerItemConfig.subscribeTags` 속성.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. 빈 문자열 벡터를 만듭니다.

   ```js
   var adTags= [];
   ```

1. 사용자 지정 광고 태그 이름을 이 벡터에 추가합니다.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. 업데이트된 벡터를 `mediaPlayerItemConfig.adTags` 속성.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 미디어 스트림을 로드할 때 미디어 플레이어 항목 구성을 사용하십시오.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```
