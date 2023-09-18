---
description: TVSDK를 사용하여 세션 관리, 게이트 액세스 등을 위해 쿠키 헤더에 임의의 데이터를 전송할 수 있습니다.
title: 쿠키를 사용한 작업
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
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

만들기 `cookieManager` 및 를 추가하고 URI에 대한 쿠키를 cookieStore에 추가합니다.

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

MediaPlayerEvent.COOKIES_UPDATED 이벤트는 C++ 쿠키가 업데이트될 때 호출됩니다. 이 cookiesUpdatedEvent에는 쿠키에 대한 문자열 값을 반환하는 getCookieString() 메서드가 있습니다.

샘플 코드 조각은 아래에 있습니다.

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
