---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
title: 쿠키를 사용한 작업
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 쿠키를 사용한 작업 {#work-with-cookies}

TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.

다음은 일부 인증이 있는 키 서버에 대한 샘플 요청입니다.

1. 고객이 브라우저에서 웹 사이트에 로그인하고 로그인하면 이 고객이 콘텐츠를 볼 수 있는 것으로 표시됩니다.
1. 라이선스 서버에서 예상한 내용에 따라 응용 프로그램에서 인증 토큰을 생성합니다.

   이 값은 TVSDK에 전달됩니다.
1. TVSDK는 쿠키 헤더에 이 값을 설정합니다.
1. TVSDK가 키 서버에 콘텐츠 암호 해독 키를 요청하면 해당 요청에는 쿠키 헤더에 인증 값이 포함됩니다.

   키 서버는 요청이 유효하다는 것을 알고 있습니다.

쿠키로 작업하려면:

1. 만들기 `cookieManager` 및 를 추가하고 URI에 대한 쿠키를 cookieStore에 추가합니다.

   예:

   ```java
   CookieManager cookieManager=new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   >[!TIP]
   >
   >302 리디렉션이 활성화되면 광고 요청은 쿠키가 속한 도메인과는 다른 도메인으로 리디렉션될 수 있습니다.

   TVSDK가 이 쿼리 `cookieManager` 런타임 시 는 URL과 연결된 쿠키가 있는지 확인하고 자동으로 해당 쿠키를 사용합니다.

   재생 중에 애플리케이션에서 쿠키를 업데이트해야 하는 경우 를 사용하지 마십시오 `networkConfiguration.setCookieHeaders` 업데이트로서의 API는 JAVA 쿠키 저장소에서 수행됩니다.

   `networkConfiguration.setCookieHeaders` API는 쿠키를 TVSDK의 C++ CookieStore로 설정합니다.

   JAVA 쿠키를 사용하고 애플리케이션과 TVSDK 간에 공유할 때 JAVA CookieStore 를 사용하여 쿠키만 관리하십시오.

   재생이 초기화되기 전에 위에 설명된 대로 쿠키 관리자를 사용하여 쿠키를 CookieStore로 설정하십시오.

   CookieStore에 저장된 쿠키는 TVSDK에 의해 자동으로 선택됩니다.

   재생 중에 쿠키 값을 나중에 업데이트해야 하는 경우, 동일한 키와 새 값 필드를 사용하여 CookieStore의 동일한 추가 메서드를 호출하십시오.

   또한 설정됨
   `networkConfiguration.setReadSetCookieHeader`(false) 호출 전
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >이 &#39;setReadSetCookieHeader&#39;를 false로 설정한 후 JAVA 쿠키 관리자를 사용하여 키 요청에 대한 쿠키를 설정합니다.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
이 콜백 API는 C++ 쿠키(http 응답에서 제공되는 쿠키)에 업데이트가 있을 때마다 실행됩니다. 애플리케이션은 이 콜백을 수신해야 하며 JAVA로 된 네트워크 호출이 아래와 같이 쿠키를 활용할 수 있도록 이에 따라 JAVA CookieStore를 업데이트할 수 있습니다.

   ```
   private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
   @Override
   public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
   List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
   for(int i = 0; i < cookies.size(); i++)
   { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
   }
   }
   ```
