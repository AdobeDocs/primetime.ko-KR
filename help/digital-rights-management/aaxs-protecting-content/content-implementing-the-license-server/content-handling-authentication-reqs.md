---
title: 인증 요청 처리
description: 인증 요청 처리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 인증 요청 처리{#handling-authentication-requests}

다음 `AuthenticationHandler` 클래스는 인증 요청을 처리하는 데 사용됩니다. 사용자 이름/암호 인증에만 사용됩니다.

인증 토큰을 생성할 때 토큰 만료 날짜를 지정해야 합니다. 사용자 지정 속성도 토큰에 포함될 수 있습니다. 이 설정을 지정하면, 인증 토큰이 후속 요청에서 전송될 때 해당 속성이 서버에 표시됩니다. 다음을 참조하십시오 [라이선스 요청 처리](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) 사용자 지정 인증 토큰 처리에 대한 자세한 정보입니다.

처리기가 인증 요청을 읽고 다음과 같은 경우 요청 메시지를 구문 분석합니다. `parseRequest()` 이(가) 호출되었습니다. 서버 구현은 요청에서 사용자 자격 증명을 검사하고 자격 증명이 유효하면 을 생성합니다. `AuthenticationToken` 를 호출한 개체 `getRequest().generateAuthToken()`. If `AuthenticationRequestMessage.generateAuthToken()` 이(가) 전에 호출되지 않음 `close()`인증 실패 오류 코드가 전송됩니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 라이선스 서버 URL: + &quot;/flashaccess/authn/v4&quot;입니다. 프로토콜 버전 3이 클라이언트 또는 서버에서 지원하는 최대값인 경우 Adobe 액세스 클라이언트는 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/authn/v3&quot;에 인증 요청을 전송합니다. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/authn/v1&quot;로 전송됩니다.
