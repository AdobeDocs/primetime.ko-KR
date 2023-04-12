---
title: Adobe의 API 테스트 사이트를 사용하여 인증 및 인증 흐름을 테스트하는 방법
description: Adobe의 API 테스트 사이트를 사용하여 인증 및 인증 흐름을 테스트하는 방법
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Adobe의 API 테스트 사이트를 사용하여 인증 및 인증 흐름을 테스트하는 방법 {#How-to-test-auth-flows}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

AuthN 및 AuthZ 플로우를 테스트하기 위해 다음을 준비했습니다 **API 테스트 사이트** 당신이 마음대로 할 수 있습니다. 저희 지원팀이 자격 증명을 제공해 드리겠습니다. 다음에 문의하시면 됩니다 **support@tve.zendesk.com**.


## 제1부 {#part-I}

RELEASE 환경에 대해 테스트하려면 Part II로 직접 건너뜁니다.  자격 전 환경에서 테스트하려면 [Pre-Qual에서 환경 및 테스트 설정](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

## 2부

제1부를 완료한 후 다음 단계를 수행합니다.


1. 웹 페이지 열기: [스테이징 API 테스트](https://sp.auth-staging.adobe.com/apitest/api.html).
1. 다음 URL에서 액세스 Enabler 로드:
   * [스테이징을 위해 Enabler javascript 액세스](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js).
   * 또는
   * [프로덕션에 대한 Enabler javascript 액세스](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js).
   * 그런 다음 &quot;**로드 액세스 Enabler**&quot; 버튼을 클릭합니다.
1. 이제 요청자 ID 값을 &quot;(으)로 설정합니다.**requestorID**&quot;을 클릭하고 &quot;setRequestor&quot; 버튼을 클릭합니다.
1. 그런 다음 &quot;getAuthentication&quot; 단추를 누르고 표시 선택기가 표시될 때까지 기다립니다.
1. &quot;**MVPD**&quot;&quot;을 클릭합니다.
1. 자격 증명을 &quot;**MVPD**&quot; 로그인 페이지.
1. 다시 리디렉션된 후 1~3단계를 재실행합니다
1. setAuthenticationStatus에서 3단계를 다시 수행하면 값 &quot;1&quot;이 표시됩니다. 인증이 작동하지 않으면 MVPD 대화 상자가 표시됩니다.
1. 인증을 테스트하려면 자원 입력 필드에 &quot;**requestorID**&quot;을(를) 클릭하고 &quot;getAuthorization&quot; 단추를 클릭합니다.
1. 따라서 &quot;setToken&quot;-\>&quot;resource id&quot; 텍스트 상자에 리소스가 표시되고 &quot;setToken&quot;-\>&quot;token&quot; 텍스트 상자에 shortAuthorizationToken이 표시되어 authZ가 성공했음을 의미합니다.
1. 이제 &quot;로그아웃&quot; 단추를 클릭하여 토큰을 삭제할 수 있습니다.

