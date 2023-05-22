---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
title: 쿠키를 사용한 작업
exl-id: f7a64c77-7db6-4bae-b299-69267fedc673
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 쿠키를 사용한 작업{#work-with-cookies}

TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.

다음은 키 서버에 대한 요청을 수행할 때 일부 유형의 인증을 사용하는 예입니다.

1. 고객이 브라우저에 웹 사이트에 로그인하면 콘텐츠를 볼 수 있다는 로그인 정보가 표시됩니다.
1. 응용 프로그램은 라이선스 서버에 필요한 것을 기반으로 인증 토큰을 생성합니다. 해당 값을 TVSDK에 전달합니다.
1. TVSDK는 쿠키 헤더에 해당 값을 설정합니다.
1. TVSDK가 키 서버에 콘텐츠 암호 해독용 키 가져오기를 요청하면 해당 요청에는 쿠키 헤더에 인증 값이 포함되어 키 서버는 요청이 유효하다는 것을 알게 됩니다.

쿠키로 작업하려면:

1. 사용 `cookieHeaders` 의 속성 `NetworkConfiguration` 쿠키를 설정합니다. 다음 `cookieHeaders` 속성은 메타데이터 개체이며 쿠키 헤더에 포함할 이 개체에 키 값 쌍을 추가할 수 있습니다.

   예:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   기본적으로 쿠키 헤더는 키 요청과만 전송됩니다. 모든 요청과 함께 쿠키 헤더를 보내려면 `NetworkConfiguration` 속성 `useCookieHeadersForAllRequests` true로 설정합니다.

1. 을 확인하려면 `NetworkConfiguration` 작동, 메타데이터로 설정:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 을(를) 만들 때 이전 단계의 메타데이터를 제공합니다. `MediaResource`.

   예를 들어 `createFromURL` 메서드에서 다음 정보를 입력합니다.

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
