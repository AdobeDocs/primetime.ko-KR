---
description: TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.
seo-description: TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.
seo-title: 사용자 정의 태그 구독
title: 사용자 정의 태그 구독
uuid: fe8ba34d-66fc-43bb-b98e-659c1702d1e0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---


# 사용자 지정 태그 구독{#subscribe-to-custom-tags}

TVSDK는 컨텐츠 매니페스트에서 이러한 개체가 나타날 때마다 구독 태그의 TimedMetadata 개체를 준비합니다.

재생을 시작하기 전에 태그에 가입해야 합니다.
HLS 매니페스트의 사용자 지정 태그에 대한 알림을 받으려면:

사용자 지정 태그가 포함된 배열을 `MediaPlayerItemConfig`의 `setSubscribedTags`으로 전달하여 사용자 지정 광고 태그 이름을 전역적으로 설정합니다.

>[!IMPORTANT]
>
>HLS 스트림을 사용하여 작업할 때는 `#` 접두어를 포함해야 합니다.

예:

```java
String[] array = new String[3]; 
array[0] = "#EXT-X-ASSET"; 
array[1] = "#EXT-X-BLACKOUT"; 
array[2] = "#EXT-OATCLS-SCTE35"; 
MediaPlayerItemConfig.setSubscribedTags(array);
```

