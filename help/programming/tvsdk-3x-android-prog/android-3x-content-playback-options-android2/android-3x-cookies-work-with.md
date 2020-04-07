---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
seo-description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
seo-title: 쿠키 작업
title: 쿠키 작업
uuid: 618bc59a-032d-445e-a867-ed2bf260570d
translation-type: tm+mt
source-git-commit: 5ada8632a7a5e3cb5d795dc42110844244656095

---


# 쿠키 작업 {#work-with-cookies}

TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.

다음은 몇 가지 인증을 통해 키 서버에 대한 샘플 요청입니다.

1. 고객이 브라우저에서 웹 사이트에 로그인하면 해당 고객이 콘텐츠를 볼 수 있음을 나타내는 로그인이 표시됩니다.
1. 라이센스 서버에서 요구하는 내용에 따라 응용 프로그램에서 인증 토큰을 생성합니다.

   이 값은 TVSDK로 전달됩니다.
1. TVSDK는 쿠키 헤더에 이 값을 설정합니다.
1. TVSDK가 키 서버에 컨텐트를 해독하기 위한 키를 가져오도록 요청하는 경우, 요청에는 쿠키 헤더의 인증 값이 포함됩니다.

   키 서버는 요청이 유효하다는 것을 알고 있습니다.

쿠키를 사용하여 작업하려면:

1. 쿠키를 `cookieManager` 만들고 cookieStore에 URI에 대한 쿠키를 추가합니다.

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
   >302 리디렉션이 활성화되면, 광고 요청이 쿠키가 속한 도메인과 다른 도메인으로 리디렉션될 수 있습니다.

   TVSDK는 런타임 `cookieManager` 시 이를 쿼리하고 URL과 연결된 쿠키가 있는지 확인하고 이러한 쿠키를 자동으로 사용합니다.

   재생하는 동안 애플리케이션에서 쿠키를 업데이트해야 하는 경우 API를 사용하지 마십시오. `networkConfiguration.setCookieHeaders` 업데이트는 JAVA 쿠키 저장소에서 발생합니다.

   `networkConfiguration.setCookieHeaders` API 파섹

   JAVA 쿠키를 사용하고 Application과 TVSDK 간에 공유할 때는 JAVA CookieStore를 사용하여 쿠키만 관리합니다.

   재생이 초기화되기 전에 위에 설명된 바와 같이 쿠키 관리자를 사용하여 쿠키를 CookieStore로 설정하십시오.

   CookieStore에 저장된 쿠키는 TVSDK에서 자동으로 선택됩니다.

   재생 중에 쿠키 값을 나중에 업데이트해야 하는 경우 동일한 키와 새 값 필드를 사용하여 CookieStore의 동일한 추가 메서드를 호출합니다.

   설정
   `networkConfiguration.setReadSetCookieHeader`(false)호출 전
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >이 &#39;setReadSetCookieHeader&#39;를 false로 설정한 후 JAVA 쿠키 관리자를 사용하여 키 요청에 대한 쿠키를 설정합니다.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
이 콜백 API는 C++ 쿠키(http 응답에서 오는 쿠키)에 업데이트가 있을 때마다 실행됩니다. 애플리케이션은 이 콜백을 수신해야 하며 JAVA의 네트워크 호출이 아래와 같이 쿠키를 활용할 수 있도록 JAVA CookieStore를 적절히 업데이트할 수 있습니다.

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
