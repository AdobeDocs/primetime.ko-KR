---
title: 인증 요청 처리
description: 인증 요청 처리
copied-description: true
exl-id: 64d23db0-254d-46b1-8317-ba0381509b44
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 인증 요청 처리 {#handle-authentication-requests}

다음 `AuthenticationHandler` 클래스는 인증 요청을 처리하는 데 사용됩니다. 사용자 이름/암호 인증에만 사용됩니다.

인증 토큰을 생성할 때 토큰 만료 날짜를 지정해야 합니다. 사용자 지정 속성도 토큰에 포함될 수 있습니다. 이 설정을 지정하면, 인증 토큰이 후속 요청에서 전송될 때 해당 속성이 서버에 표시됩니다. 다음을 참조하십시오 [라이선스 요청 처리](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) 사용자 지정 인증 토큰 처리에 대한 자세한 정보입니다.

처리기가 인증 요청을 읽고 다음과 같은 경우 요청 메시지를 구문 분석합니다. `parseRequest()` 이(가) 호출되었습니다. 서버 구현은 요청에서 사용자 자격 증명을 검사하고 자격 증명이 유효하면 을 생성합니다. `AuthenticationToken` 를 호출한 개체 `getRequest().generateAuthToken()`. If `AuthenticationRequestMessage.generateAuthToken()` 이(가) 전에 호출되지 않음 `close()`인증 실패 오류 코드가 전송됩니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 라이선스 서버 URL: + &quot; [!DNL /flashaccess/authn/v4]&quot;. 프로토콜 버전 3이 클라이언트나 서버에서 지원하는 최대값인 경우 Adobe Primetime DRM 클라이언트는 인증 요청을 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;
