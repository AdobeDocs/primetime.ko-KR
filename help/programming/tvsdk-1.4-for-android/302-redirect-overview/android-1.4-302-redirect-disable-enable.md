---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 응용 프로그램에서 더 효과적으로 부하 균형을 맞출 수 있습니다.
title: 302 리디렉션 최적화 비활성화 또는 활성화
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# HTTP 302 리디렉션 최적화 {#http-302-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 응용 프로그램에서 더 효과적으로 부하 균형을 맞출 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 302 최적화가 플레이어에서 활성화된 경우 해당 매니페스트의 자산에 대해 수행된 후속 요청은 최종 도메인 위치를 사용하므로 추가적인 302개의 응답을 피합니다.

이 기능은 기본적으로 활성화되어 있으며 이 설정을 변경할 수 있습니다.

## 302 리디렉션 최적화 비활성화 또는 활성화{#disable-or-enable-redirect-optimization}

`useRedirectedUrl` 속성을 사용하여 302 리디렉션을 설정(true) 또는 해제(false)합니다.
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

