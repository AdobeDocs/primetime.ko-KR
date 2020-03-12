---
seo-title: 인증 요청 처리
title: 인증 요청 처리
uuid: abcb9cf6-668e-405c-9659-9ed1bcc33024
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 인증 요청 처리 {#handle-authentication-requests}

이 `AuthenticationHandler` 클래스는 인증 요청을 처리하는 데 사용됩니다. 사용자 이름/암호 인증에만 사용됩니다.

인증 토큰을 생성할 때 토큰 만료 날짜를 지정해야 합니다. 사용자 지정 속성은 토큰에 포함될 수도 있습니다. 설정하면 인증 토큰이 후속 요청에서 전송될 때 해당 속성이 서버에 표시됩니다. 사용자 [정의 인증 토큰 처리에 대한 자세한 내용은 라이선스 요청](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) 처리를 참조하십시오.

핸들러는 인증 요청을 읽고 요청 메시지를 `parseRequest()` 호출할 때 구문 분석합니다. 서버 구현은 요청에서 사용자 자격 증명을 검사하고 자격 증명이 유효한 경우 호출을 통해 `AuthenticationToken` 개체를 생성합니다 `getRequest().generateAuthToken()`. 이전에 `AuthenticationRequestMessage.generateAuthToken()` 호출되지 않으면 인증 실패 오류 코드가 `close()`전송됩니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 클라이언트 및 서버 지원 프로토콜 버전 5가 모두 지원되는 경우 요청 URL은 &quot;메타데이터의 라이센스 서버 URL:+ &quot; [!DNL /flashaccess/authn/v4]&quot;. 프로토콜 버전 3이 클라이언트 또는 서버에서 지원되는 최대 버전인 경우 Adobe Primetime DRM 클라이언트는 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;에 대한 인증 요청을 수락합니다. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;로 전송됩니다.

