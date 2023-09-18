---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션이 로드 밸런스를 보다 효과적으로 조정할 수 있습니다.
title: 302 리디렉션 최적화 비활성화 또는 활성화
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# HTTP 302 리디렉션 최적화 {#http-302-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션이 로드 밸런스를 보다 효과적으로 조정할 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 플레이어에서 302 최적화가 활성화되어 있으면 해당 매니페스트의 자산에 대해 수행된 후속 요청에서는 최종 도메인 위치를 사용하므로 302 응답이 더 이상 발생하지 않습니다.

이 기능은 기본적으로 활성화되어 있으며 이 설정을 변경할 수 있습니다.

## 302 리디렉션 최적화 비활성화 또는 활성화{#disable-or-enable-redirect-optimization}

사용 `useRedirectedUrl` 302 리디렉션을 켜거나(true) 끄는(false) 속성입니다.
예:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration as Metadata: 
MetadataNode resourceMetadata = new MetadataNode();  
resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                         networkConfiguration); 
 
//Call MediaResource.createFromURL to set the metadata: 
MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
  
//Load the resource 
mediaPlayer.replaceCurrentItem(resource);
```
