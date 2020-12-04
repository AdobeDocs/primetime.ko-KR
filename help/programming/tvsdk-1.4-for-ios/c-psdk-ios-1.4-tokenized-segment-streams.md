---
description: CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 때때로 매니페스트에 인증 토큰을 사용하고 검증을 위해 세그먼트 요청을 사용할 수 있습니다. 이러한 토큰은 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다.
seo-description: CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 때때로 매니페스트에 인증 토큰을 사용하고 검증을 위해 세그먼트 요청을 사용할 수 있습니다. 이러한 토큰은 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다.
seo-title: 토큰화된 세그먼트 스트림
title: 토큰화된 세그먼트 스트림
uuid: b17bb5bc-2029-4113-ac44-b1d30aa08ca6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# 토큰화된 세그먼트 스트림{#tokenized-segment-streams}

CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 때때로 매니페스트에 인증 토큰을 사용하고 검증을 위해 세그먼트 요청을 사용할 수 있습니다. 이러한 토큰은 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다.

마스터 매니페스트(m3u8) 응답에서 쿠키로 제공된 토큰은 세그먼트 요청이 동일한 도메인에 대한 경우에도 세그먼트(ts) 요청과 공유되지 않습니다. 세그먼트 요청에서 이러한 쿠키의 공유를 활성화하려면 플레이어 항목에 제공된 `PTMetadata` 인스턴스의 다음 속성을 설정합니다. 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

스트림이 재생을 시작하기 전에 마스터 매니페스트(m3u8)에 대한 추가 요청이 수행됩니다.

>[!IMPORTANT]
>
>이 쿠키 공유 기능은 iOS 8 이상을 실행하는 장치에서만 지원됩니다.

