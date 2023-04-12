---
title: Amazon FireOS SSO(Clientless API Cookbook 사용)
description: Amazon FireOS SSO(Clientless API Cookbook 사용)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# Amazon FireOS SSO(Clientless API Cookbook 사용) {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>

## 소개 {#Introduction}

이 문서에서는 클라이언트 없는 API를 사용하여 Amazon의 SSO 버전의 Adobe Primetime 인증 흐름을 구현하는 지침을 제공합니다. 이 문서의 첫 번째 부분에서는 이미 구현에 익숙하고 경험이 풍부한 많은 파트너를 위해 아키텍처의 Amazon 버전 특성에 중점을 둡니다.

문서의 두 번째 부분에서는 Adobe Primetime Authentication Clientless API를 구현하는 주요 단계를 다룹니다.

Clientless 솔루션 작동 방식에 대한 광범위한 기술 개요는 다음을 참조하십시오. [REST API 개요](/help/authentication/rest-api-overview.md). Adobe 는 전체 아키텍처 및 첫 번째 구현에 대한 지원을 위해 선호되는 연락처입니다.

## Amazon Clientless SSO {#AMZ-Clientless-SSO}

### 높은 수준의 아키텍처 {#High-Level-Arch}

Amazon Clientless SSO 구현은 간단하며 대부분 일반 Adobe Primetime Authentication clientless API와 동일합니다.

Amazon SDK를 사용하여 개인화된 페이로드를 검색하고 Adobe 클라이언트 없는 API를 호출할 때 사용해야 합니다.

페이로드가 인식되고 인증된 세션에 해당하는 경우 클라이언트 없는 API는 세션의 토큰을 사용하여 즉시 반환됩니다.

### Amazon SDK를 사용하는 애플리케이션을 빌드하는 방법 {#Build-entries}

* 최신 다운로드 및 복사 [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) /SSOEnabler 폴더를 앱 디렉토리와 병렬로
* 라이브러리를 사용하도록 매니페스트/gradle 파일을 업데이트합니다.

   **매니페스트 파일에 다음 줄을 추가합니다.**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **gradle 파일 항목:**

   저장소 아래에서 다음을 수행합니다.

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   종속성 아래에 다음을 추가합니다.

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* Amazon Companion App이 없는 처리:

   응용 프로그램이 실행 중인 Amazon 장치에 파트너가 없으면 다음 클래스에서 런타임 시 ClassNotFoundException이 발생합니다. `com.amazon.ottssotokenlib.SSOEnabler`.

   이 경우 페이로드 단계를 건너뛰고 일반 PrimeTime 플로우에서 폴백하면 됩니다. SSO가 활성화되지 않지만 일반 인증 흐름이 정상적으로 수행됩니다.

</br>

### Amazon SDK를 사용하여 Amazon SSO 페이로드를 가져오는 방법 {#UseAmazonSSO}

응용 프로그램 초기화 중에 SOEnabler 인스턴스를 가져옵니다. 애플리케이션 아키텍처를 기반으로 동기식 또는 비동기식 구현 중 하나를 결정해야 합니다.

어떤 이유로든 API 호출이 페이로드를 반환하지 않는 경우 일반 비 SSO 흐름을 사용하고 Amazon 및 Adobe 파트너에게 문의하여 조사하십시오.

**비동기 API**

* SSO Enabler 인스턴스 가져오기:

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* 콜백 설정 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * 성공 응답 번들에는 다음이 포함됩니다.
      * 키 &quot;SSOTtoken&quot;이 있는 문자열로 SSO 토큰
   * 실패 응답 번들에는 다음이 포함됩니다.
      * 오류 코드가 &quot;ErrorCode&quot; 키가 있는 int로 표시됩니다.
      * 오류 설명(&quot;ErrorDescription&quot; 키가 있는 문자열)


* SSO 토큰 가져오기

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* 이 API는 초기화 중에 설정된 콜백을 통해 응답을 제공합니다.

   **Ex**. init 중에 생성된 단일 인스턴스를 사용하여 호출

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**동기 API**

* SSO Enabler 인스턴스를 가져오고 콜백을 설정합니다.

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* SSO 토큰 가져오기

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * 이 API는 호출자 스레드를 차단하며 결과 번들로 응답합니다. 이 호출은 동기 호출이므로 주 스레드에 사용하지 마십시오.

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * 값(밀리초)입니다. 설정된 경우 동기화 API에 대한 기본 시간 제한 값 1분을 재정의합니다.



### Dynamic Client Registration을 사용하기 위한 Adobe Primetime Clientless API 업데이트 {#clientlessdcr}

첫 번째 구현인 경우 **Clientless 기술 개요** 지원이 필요한 경우 Adobe에 문의하십시오.

Adobe Clientless API를 사용하려면 Adobe 서버를 호출하기 위해 애플리케이션에서 Dynamic Client Registration을 사용해야 합니다.

* 애플리케이션에서 Dynamic Client Registration을 사용하려면 다음 지침을 따르십시오. [ Dynamic Client Registration Management에서 애플리케이션을 등록합니다](/help/authentication/dynamic-client-registration-management.md).

* Dynamic Client Registration API를 구현하여 Adobe Primetime 서버에 인증 및 권한 부여 요청을 수행하려면 다음 지침을 따르십시오. [동적 클라이언트 등록 API](/help/authentication/dynamic-client-registration-api.md) .

### Amazon SSO를 사용하기 위한 Adobe Primetime Clientless API 업데이트 {#clientlesssso}

Amazon SDK에서 가져온 Amazon SSO 페이로드는 Adobe Primetime 인증 종단점에 대한 요청에 있어야 합니다.

```
      /adobe-services/*
      /reggie/*
      /api/*
```


모든 Primetime 인증 엔드포인트는 장치 범위 식별자 또는 플랫폼 범위 식별자(Amazon SSO 페이로드에 있음)를 수신하는 다음 메서드를 지원합니다.

* 헤더 : &quot;Adobe-제목-토큰&quot;
* 쿼리 매개 변수 로서: &quot;ast&quot;
* post 매개 변수 로서 : &quot;ast&quot;


>[!NOTE]
>
>장치 범위 식별자 또는 플랫폼 범위 식별자를 쿼리/post 매개 변수로 보낸 경우 요청 서명을 생성할 때 포함해야 합니다.

>[!NOTE]
>
>쿼리 매개 변수 &quot;ast&quot;를 사용하면 전체 url이 매우 길어지고 거부될 수 있습니다. /authenticate 호출에서 /regcode 호출에 제공되었을 때 이 매개 변수를 건너뛸 수 있습니다

**예:**

**사용자 지정 헤더로 보내기**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**쿼리 매개 변수로 보내기**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**post 매개 변수로 전송**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>Amazon SSO가 없거나 잘못된 경우 Adobe Primetime 인증이 속성을 무시하고 SSO가 없는 것처럼 호출이 실행됩니다.
