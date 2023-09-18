---
description: TVSDK는 HTTPS를 통한 보안 전달을 도입합니다.
title: HTTPS를 통한 보안 게재
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# HTTPS를 통한 보안 게재 {#secure-delivery-https}

Adobe Primetime TVSDK는 TVSDK에서 시작되는 모든 호출에 대해 HTTPS 전달을 지원합니다.

* Auditude 광고 서버 호출
* CRS 요청
* DRM 라이센스 호출
* Video Analytics Ping
* 청구 Ping

이 기능을 사용하려면 위의 요청을 제공하도록 구성된 서버가 HTTPS를 지원하는지 확인하십시오.

이 새 동작은 기본적으로 활성화되어 있지 않습니다. 호출 전 보안 게재를 활성화하려면 다음을 사용하십시오. `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
