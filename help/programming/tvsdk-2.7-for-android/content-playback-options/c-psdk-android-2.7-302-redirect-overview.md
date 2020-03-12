---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.
seo-description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.
seo-title: HTTP 302 리디렉션 최적화
title: HTTP 302 리디렉션 최적화
uuid: 4bee0555-ae46-47c1-a067-206ad7ca8883
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# HTTP 302 리디렉션 최적화 {#http-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 302 최적화가 플레이어에서 활성화된 경우, 해당 매니페스트의 자산에 대해 수행된 후속 요청은 최종 도메인 위치를 사용하므로 302개의 응답이 추가로 발생하지 않습니다. 이 기능은 기본적으로 활성화되어 있으므로 이 설정을 변경할 수 있습니다.

## 302 리디렉션 최적화 비활성화 또는 활성화 {#section_8977448B268E41D69A8F75B60EB9DA3B}

302 `useRedirectedUrl` 리디렉션을 설정() `true``false`또는 해제()하려면 속성을 사용합니다.

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

예:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```

