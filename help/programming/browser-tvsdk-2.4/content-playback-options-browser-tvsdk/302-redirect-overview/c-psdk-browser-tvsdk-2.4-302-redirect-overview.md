---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.
seo-description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.
seo-title: HTTP 302 리디렉션 최적화
title: HTTP 302 리디렉션 최적화
uuid: d3009c6c-320a-4c0f-b6ba-bf6473049823
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# HTTP 302 리디렉션 최적화 {#http-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 302 최적화가 플레이어에서 활성화된 경우, 해당 매니페스트의 자산에 대해 수행된 후속 요청은 최종 도메인 위치를 사용하므로 302개의 응답이 추가로 발생하지 않습니다. 이 기능은 기본적으로 활성화되어 있으므로 이 설정을 변경할 수 있습니다.

>[!IMPORTANT]
>
>이 기능은 `responseURL` `XMLHttpRequest` 객체의 속성을 지원하는 인증된 브라우저에서만 지원됩니다.

Flash 폴백의 경우 다음 정보를 기억하십시오.

* 최종 사용자는 Adobe Flash Player 버전 23 이상을 설치해야 합니다.
* 스트림 무결성이 비활성화된 경우 인증된 브라우저에서만 302 리디렉션이 지원됩니다.

## 302 리디렉션 최적화 비활성화 {#disabling-redirect-optimization}

useRedirectedUrl 속성을 사용하여 302 리디렉션(true)을 활성화하거나 비활성화(false)할 수 있습니다.

예:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
