---
description: 302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 응용 프로그램에서 더 효과적으로 부하 균형을 맞출 수 있습니다.
title: HTTP 302 리디렉션 최적화
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# HTTP 302 리디렉션 최적화{#http-redirect-optimization}

302 리디렉션 최적화는 302 리디렉션 응답 수를 최소화하므로 응용 프로그램에서 더 효과적으로 부하 균형을 맞출 수 있습니다.

기본 매니페스트 요청이 리디렉션되고 302 최적화가 플레이어에서 활성화된 경우 해당 매니페스트의 자산에 대해 수행된 후속 요청은 최종 도메인 위치를 사용하므로 추가적인 302개의 응답을 피합니다.

이 기능은 기본적으로 비활성화되며 이 설정을 변경할 수 있습니다.

이 기능을 활성화하면 다음 조건 중 *모두*&#x200B;가 참인 경우에만 올바르게 작동합니다.그렇지 않으면 리디렉션 최적화가 발생하지 않으며 302 응답이 계속 발생합니다.

* 응용 프로그램이 `-swf-version` 21 이상을 사용하여 Adobe Flash Player 11.8용으로 컴파일되었습니다.
* 최종 사용자에게 Adobe Flash Player 11.8 이상이 설치되어 있습니다.

>[!IMPORTANT]
>
>쿠키가 광고 요청과 함께 전달되도록 하려면 302 리디렉션을 비활성화합니다. 302 리디렉션이 활성화되면, 광고 요청이 쿠키가 발생한 도메인과 다른 도메인으로 리디렉션될 수 있습니다.

## 302 리디렉션 최적화 비활성화 또는 활성화 {#section_D6687FC44C61446F878008B629A5FA19}

`useRedirectedUrl` 속성을 사용하여 302 리디렉션을 설정(true) 또는 해제(false)합니다.

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

