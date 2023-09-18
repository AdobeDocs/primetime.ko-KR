---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
title: 쿠키를 사용한 작업
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '246'
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

1. 만들기 `cookieManager` 및 를 추가하여 URI에 대한 쿠키를 `cookieStore`.

   예:

   >[!IMPORTANT]
   >
   >302 리디렉션이 활성화되면 광고 요청은 쿠키가 속한 도메인과는 다른 도메인으로 리디렉션될 수 있습니다.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK는 런타임 시 이 cookieManager를 쿼리하고, URL과 연결된 쿠키가 있는지 확인하고, 이러한 쿠키를 자동으로 사용합니다.

   또 다른 옵션은 `cookieHeaders` 위치: `NetworkConfiguration` 요청에 사용할 임의의 쿠키 헤더 문자열을 설정합니다. 기본적으로 이 쿠키 헤더는 키 요청과 함께 전송됩니다. 모든 요청과 함께 쿠키 헤더를 보내려면 `NetworkConfiguration` 방법 `setUseCookieHeadersForAllRequests`:

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
