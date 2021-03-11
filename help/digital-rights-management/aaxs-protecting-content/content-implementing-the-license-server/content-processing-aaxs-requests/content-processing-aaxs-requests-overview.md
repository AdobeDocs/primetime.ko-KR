---
title: 개요
description: 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# 개요{#overview}

요청을 처리하는 일반적인 방법은 핸들러를 만들고, 요청을 구문 분석하고, 응답 데이터 또는 오류 코드를 설정하고, 핸들러를 닫는 것입니다.

단일 요청/응답 상호 작용을 처리하는 데 사용되는 기본 클래스는 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`입니다. `HandlerConfiguration` 클래스의 인스턴스를 사용하여 핸들러를 초기화합니다. `HandlerConfiguration` 전송 자격 증명, 타임스탬프 허용 한도, 정책 업데이트 목록 및 해지 목록을 포함하는 서버 구성 정보를 저장합니다.핸들러는 요청 데이터를 읽고 요청을 의 인스턴스로 구문 분석합니다 `RequestMessageBase`. 호출자는 요청의 정보를 검사하여 오류를 반환할지 또는 성공적인 응답을 반환할지 결정할 수 있습니다(`RequestMessageBase`의 하위 클래스는 응답 데이터를 설정하는 방법을 제공합니다).

요청이 성공하면 응답 데이터를 설정합니다.그렇지 않으면 실패 시 `RequestMessageBase.setErrorData()`을(를) 불러옵니다. 항상 `close()` 메서드를 호출하여 구현을 종료합니다.( `try` 문의 `finally` 블록에서 `close()`을 호출하는 것이 좋습니다.) 핸들러를 호출하는 방법에 대한 예는 `MessageHandlerBase` API 참조 설명서를 참조하십시오.

>[!NOTE]
>
>HTTP 상태 코드 200(OK)은 처리기가 처리하는 모든 요청에 응답하여 전송해야 합니다. 서버 오류로 인해 핸들러를 만들 수 없는 경우 서버가 500(내부 서버 오류)과 같은 다른 상태 코드로 응답할 수 있습니다.

클라이언트는 패키지 시간에 지정된 라이센스 서버 URL을 라이센스 서버로 전송된 모든 요청에 대한 기본 URL로 사용합니다. 예를 들어 서버 URL이 &quot;ht<span></span>tps://licenseserver.com/path&quot;으로 지정된 경우 클라이언트는 &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/...&quot;에 요청을 보냅니다. 각 요청 유형에 사용되는 특정 경로에 대한 자세한 내용은 다음 섹션을 참조하십시오. 라이센스 서버를 구현할 때 서버가 각 요청 유형에 필요한 경로에 응답해야 합니다.

라이센스 요청에는 인증 토큰이 포함될 수 있습니다. 사용자 이름/암호 인증을 사용한 경우 요청에 `AuthenticationHandler`에서 생성된 `AuthenticationToken`이 포함될 수 있으며 SDK는 라이선스를 발급하기 전에 토큰이 유효한지 확인합니다.
