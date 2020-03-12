---
description: TVSDK는 HTTPS를 통한 안전한 전달을 제공합니다.
seo-description: TVSDK는 HTTPS를 통한 안전한 전달을 제공합니다.
seo-title: HTTPS를 통한 안전한 전달
title: HTTPS를 통한 안전한 전달
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9

---


# HTTPS를 통한 안전한 전달 {#secure-delivery-https}

Adobe Primetime TVSDK는 TVSDK에서 오는 모든 호출에 대해 HTTPS 제공을 지원합니다. 여기에는

* Auditude 광고 서버 호출
* CRS 요청
* DRM 라이선스 호출
* 비디오 분석 핑
* 청구 설정

이 기능을 사용하려면 위의 요청을 제공하도록 구성된 서버가 HTTPS를 지원하는지 확인하십시오.

이 새 동작은 기본적으로 활성화되지 않습니다. 다음을 사용하여 `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
