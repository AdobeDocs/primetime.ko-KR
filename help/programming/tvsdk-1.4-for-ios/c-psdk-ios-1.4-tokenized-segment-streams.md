---
description: CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 경우에 따라 확인을 위해 매니페스트 및 세그먼트 요청에 인증 토큰을 사용할 수 있습니다. 이러한 토큰은 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다.
title: 토큰화된 세그먼트 스트림
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 토큰화된 세그먼트 스트림{#tokenized-segment-streams}

CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 경우에 따라 확인을 위해 매니페스트 및 세그먼트 요청에 인증 토큰을 사용할 수 있습니다. 이러한 토큰은 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다.

마스터 매니페스트(m3u8) 응답에서 쿠키로 제공되는 토큰은 세그먼트 요청이 동일한 도메인에 대한 것일 때에도 세그먼트(ts) 요청과 공유되지 않습니다. 세그먼트 요청에서 이러한 쿠키를 공유할 수 있게 하려면 `PTMetadata` 플레이어 항목에 제공된 인스턴스: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

스트림 재생이 시작되기 전에 마스터 매니페스트(m3u8)에 대한 추가 요청이 수행됩니다.

>[!IMPORTANT]
>
>이 쿠키 공유 기능은 iOS 8 이상을 실행하는 장치에서만 지원됩니다.
