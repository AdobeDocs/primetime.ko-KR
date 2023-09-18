---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션이 로드 밸런스를 보다 효과적으로 조정할 수 있습니다.
title: HTTP 302 리디렉션 최적화
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# HTTP 302 리디렉션 최적화 {#http-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션이 로드 밸런스를 보다 효과적으로 조정할 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 플레이어에서 302 최적화가 활성화되어 있으면 해당 매니페스트의 자산에 대해 수행된 후속 요청에서는 최종 도메인 위치를 사용하므로 302 응답이 더 이상 발생하지 않습니다. 이 기능은 기본적으로 활성화되어 있으며 이 설정을 변경할 수 있습니다.

>[!IMPORTANT]
>
>이 기능은 를 지원하는 인증된 브라우저에서만 지원됩니다. `responseURL` 의 속성 `XMLHttpRequest` 개체.

Flash 폴백의 경우 다음 정보를 기억하십시오.

* 최종 사용자는 Adobe Flash Player 버전 23 이상이 설치되어 있어야 합니다.
* 스트림 무결성이 비활성화되면 인증된 브라우저에서만 302 리디렉션이 지원됩니다.

## 302 리디렉션 최적화 비활성화 {#disabling-redirect-optimization}

useRedirectedUrl 속성을 사용하여 302 리디렉션(true) 또는 비활성화(false)를 활성화할 수 있습니다.

예:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
