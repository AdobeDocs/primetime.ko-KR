---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
seo-description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
seo-title: 쿠키 작업
title: 쿠키 작업
uuid: 7586a5a7-9914-403b-86a9-fbdd28664b07
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 쿠키 작업{#work-with-cookies}

TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.

다음은 키 서버에 요청을 할 때 일부 인증 유형을 사용하는 예입니다.

1. 고객이 브라우저에서 웹 사이트에 로그인하면 해당 로그인에 컨텐츠가 표시될 수 있습니다.
1. 응용 프로그램은 라이센스 서버에서 요구하는 내용을 기반으로 인증 토큰을 생성합니다. 이 값을 TVSDK로 전달합니다.
1. TVSDK는 쿠키 헤더에 해당 값을 설정합니다.
1. TVSDK가 키 서버에 컨텐트를 해독하기 위한 키를 가져오도록 요청하는 경우, 해당 요청에는 쿠키 헤더에 인증 값이 포함되어 있으므로 키 서버는 요청이 유효하다는 것을 알고 있습니다.

쿠키를 사용하여 작업하려면:

1. 의 `cookieHeaders` 속성을 사용하여 쿠키를 `NetworkConfiguration` 설정합니다. 이 `cookieHeaders` 속성은 메타데이터 개체이며, 쿠키 헤더에 포함할 키 값 쌍을 이 개체에 추가할 수 있습니다.

   예:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   기본적으로 쿠키 헤더는 키 요청과 함께 전송됩니다. 모든 요청과 함께 쿠키 헤더를 전송하려면 `NetworkConfiguration` 속성을 true `useCookieHeadersForAllRequests` 로 설정합니다.

1. 이를 `NetworkConfiguration` 수행하려면 다음 메타데이터를 메타데이터로 설정합니다.

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 를 만들 때 이전 단계의 메타데이터를 제공합니다 `MediaResource`.

   예를 들어 `createFromURL` 메서드를 사용하는 경우 다음 정보를 입력합니다.

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

