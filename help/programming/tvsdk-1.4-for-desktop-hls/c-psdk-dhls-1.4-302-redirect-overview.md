---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.
seo-description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.
seo-title: HTTP 302 리디렉션 최적화
title: HTTP 302 리디렉션 최적화
uuid: 58593d5f-a639-4d87-9589-dba6b2dbba38
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# HTTP 302 리디렉션 최적화{#http-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 애플리케이션의 로드 밸런스를 보다 효과적으로 활용할 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 302 최적화가 플레이어에서 활성화된 경우, 해당 매니페스트의 자산에 대해 수행된 후속 요청은 최종 도메인 위치를 사용하므로 302개의 응답이 추가로 발생하지 않습니다.

이 기능은 기본적으로 비활성화되며 이 설정을 변경할 수 있습니다.

이 기능을 활성화하면 다음 *모든* 조건이 참인 경우에만 올바르게 작동합니다.그렇지 않으면 리디렉션 최적화가 발생하지 않으며 302 응답이 계속 발생합니다.

* 애플리케이션이 Adobe Flash Player 11.8용으로 21 `-swf-version` 이상 버전을 사용하여 컴파일되었습니다.
* 최종 사용자는 Adobe Flash Player 11.8 이상이 설치되어 있습니다.

>[!IMPORTANT]
>
>쿠키가 광고 요청과 함께 전달되도록 하려면 302 리디렉션을 비활성화합니다. 302 리디렉션이 활성화되면 광고 요청이 쿠키가 발생한 도메인과 다른 도메인으로 리디렉션될 수 있습니다.

## 302 리디렉션 최적화 비활성화 또는 활성화 {#section_D6687FC44C61446F878008B629A5FA19}

302 리디렉션을 설정(true)하거나 설정 해제(false)하려면 `useRedirectedUrl` 속성을 사용합니다.

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

예:

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```

