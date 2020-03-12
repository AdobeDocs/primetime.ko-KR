---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
seo-description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
seo-title: 쿠키 작업
title: 쿠키 작업
uuid: f060b520-ceec-48ca-929f-683566fe6ae7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 쿠키 작업{#work-with-cookies}

TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.

다음은 키 서버에 요청을 할 때 일부 인증 유형을 사용하는 예입니다.

1. 고객이 브라우저에서 웹 사이트에 로그인하면 해당 로그인에 컨텐츠가 표시될 수 있습니다.
1. 응용 프로그램은 라이센스 서버에서 요구하는 내용을 기반으로 인증 토큰을 생성합니다. 이 값을 TVSDK로 전달합니다.
1. TVSDK는 쿠키 헤더에 해당 값을 설정합니다.
1. TVSDK가 키 서버에 컨텐트를 해독하기 위한 키를 가져오도록 요청하는 경우, 해당 요청에는 쿠키 헤더에 인증 값이 포함되어 있으므로 키 서버는 요청이 유효하다는 것을 알고 있습니다.

쿠키를 사용하여 작업하려면:

1. URI에 대한 쿠키를 `cookieManager` 만들고 `cookieStore`추가합니다.

   예:

   >[!IMPORTANT]
   >
   >302 리디렉션이 활성화되면, 광고 요청이 쿠키가 속한 도메인과 다른 도메인으로 리디렉션될 수 있습니다.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK는 런타임에 이 cookieManager를 쿼리하고 URL과 연결된 쿠키가 있는지 확인하고 자동으로 사용합니다.

   다른 옵션은 에서 `cookieHeaders` 임의의 쿠키 헤더 문자열을 `NetworkConfiguration` 설정하여 요청에 사용할 수 있도록 하는 것입니다. 기본적으로 이 쿠키 헤더는 키 요청과 함께 전송됩니다. 모든 요청과 함께 쿠키 헤더를 보내려면 `NetworkConfiguration` 방법을 `setUseCookieHeadersForAllRequests`사용합니다.

   ```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
   
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
   
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode();  
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
   
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
    // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
   ```

