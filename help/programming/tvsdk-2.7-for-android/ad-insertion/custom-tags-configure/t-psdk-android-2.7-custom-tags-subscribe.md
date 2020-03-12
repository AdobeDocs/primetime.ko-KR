---
description: TVSDK 파섹
seo-description: TVSDK 파섹
seo-title: 사용자 정의 태그 구독
title: 사용자 정의 태그 구독
uuid: 9f74b2b9-bbc9-433c-8226-2c2b68eddf7e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 사용자 정의 태그 구독 {#subscribe-to-custom-tags}

TVSDK 파섹

재생이 시작되기 전에 태그에 가입해야 합니다. HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

1. 사용자 지정 태그가 포함된 배열을 전달하여 사용자 지정 광고 태그 이름을 전체적으로 `setSubscribedTags` 설정합니다 `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >HLS 스트림을 사용하여 작업할 때는 `#` 접두사를 포함해야 합니다.

   예:

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```

