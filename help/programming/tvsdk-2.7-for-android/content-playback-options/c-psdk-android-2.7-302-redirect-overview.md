---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션이 로드 밸런스를 보다 효과적으로 조정할 수 있습니다.
title: HTTP 302 리디렉션 최적화
exl-id: fdbdc2b4-6c1a-4ab1-80e2-b5e079ffa906
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# HTTP 302 리디렉션 최적화 {#http-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션이 로드 밸런스를 보다 효과적으로 조정할 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 플레이어에서 302 최적화가 활성화되어 있으면 해당 매니페스트의 자산에 대해 수행된 후속 요청에서는 최종 도메인 위치를 사용하므로 302 응답이 더 이상 발생하지 않습니다. 이 기능은 기본적으로 활성화되어 있으며 이 설정을 변경할 수 있습니다.

## 302 리디렉션 최적화 비활성화 또는 활성화 {#section_8977448B268E41D69A8F75B60EB9DA3B}

사용 `useRedirectedUrl` 302 리디렉션을 켤 속성( `true`) 또는 해제( `false`).

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
