---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
title: 쿠키를 사용한 작업
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# {#work-with-cookies} 쿠키 작업

TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.

다음은 몇 가지 인증이 있는 키 서버에 대한 샘플 요청입니다.

1. 고객이 브라우저에서 웹 사이트에 로그인하면 해당 고객이 콘텐츠를 볼 수 있음을 나타내는 로그인이 표시됩니다.
1. 라이센스 서버에서 요구하는 내용을 기반으로 응용 프로그램에서 인증 토큰을 생성합니다.

   이 값은 TVSDK로 전달됩니다.
1. TVSDK는 쿠키 헤더에 이 값을 설정합니다.
1. TVSDK가 콘텐트의 암호를 해독하기 위한 키를 얻기 위해 키 서버에 요청을 하면 해당 요청에는 쿠키 헤더의 인증 값이 포함됩니다.

   키 서버는 요청이 유효하다는 것을 알고 있습니다.

쿠키를 사용하여 작업하려면:

`cookieManager`을(를) 만들고 URI에 대한 쿠키를 cookieStore에 추가합니다.

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

TVSDK는 이 `cookieManager`을(를) 런타임에 쿼리하고 URL과 연관된 쿠키가 있는지 확인하고 이러한 쿠키를 자동으로 사용합니다.

C++ 쿠키가 업데이트되면 MediaPlayerEvent.COOKIES_UPDATED 이벤트가 호출됩니다. 이 cookiesUpdatedEvent에는 쿠키의 문자열 값을 반환하는 getCookieString() 메서드가 있습니다.

샘플 코드 조각은 다음과 같습니다.

```
private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener()  
{ 
@Override 
public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) 
 { 
 String cookieStr = cookiesUpdatedEvent.getCookieString();  
 logger.i(LOG_TAG + "::MediaPlayer.CookiesUpdatedEventListener#onCookiesUpdated()", "cookieStr " + cookieStr);  
 }  
};
```

