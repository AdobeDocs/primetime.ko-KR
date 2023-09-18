---
title: 개요
description: 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 개요{#overview}

요청을 처리하는 일반적인 방법은 핸들러를 만들고, 요청을 구문 분석하고, 응답 데이터 또는 오류 코드를 설정하고, 핸들러를 닫는 것입니다.

단일 요청/응답 상호 작용을 처리하는 데 사용되는 기본 클래스는 다음과 같습니다. `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. 의 인스턴스 `HandlerConfiguration` 클래스를 사용하여 처리기를 초기화할 수 있습니다. `HandlerConfiguration` 전송 자격 증명, 타임스탬프 허용 오차, 정책 업데이트 목록 및 해지 목록을 포함한 서버 구성 정보를 저장합니다. 처리기는 요청 데이터를 읽고 요청을 다음 인스턴스로 구문 분석합니다. `RequestMessageBase`. 호출자는 요청의 정보를 검사하고 오류 또는 성공적인 응답을 반환할지 여부를 결정할 수 있습니다(의 하위 클래스). `RequestMessageBase` 응답 데이터를 설정하는 방법을 제공합니다).

요청이 성공하면 응답 데이터를 설정하고, 그렇지 않으면 를 호출합니다. `RequestMessageBase.setErrorData()` 실패 시. 항상 를 호출하여 구현을 종료하십시오 `close()` 메서드(권장 사항) `close()` 호출될 위치: `finally` 블록 `try` 문)을 참조하십시오. 다음을 참조하십시오. `MessageHandlerBase` 처리기를 호출하는 방법의 예를 보려면 API 참조 설명서입니다.

>[!NOTE]
>
>HTTP 상태 코드 200(OK)은 핸들러가 처리한 모든 요청에 대한 응답으로 전송되어야 합니다. 서버 오류로 인해 핸들러를 만들 수 없는 경우 서버는 500(내부 서버 오류)과 같은 다른 상태 코드로 응답할 수 있습니다.

클라이언트는 패키징 시간에 지정된 라이선스 서버 URL을 라이선스 서버에 전송된 모든 요청에 대한 기본 URL로 사용합니다. 예를 들어 서버 URL이 &quot;ht&quot;로 지정된 경우<span></span>tps://licenseserver.com/path으로 지정하면 클라이언트는 &quot;ht&quot;에 요청을 보냅니다.<span></span>tps://licenseserver.com/path/flashaccess/...&quot; 각 요청 유형에 사용되는 특정 경로에 대한 자세한 내용은 다음 섹션을 참조하십시오. 라이센스 서버를 구현할 때는 서버가 각 요청 유형에 필요한 경로에 응답해야 합니다.

라이선스 요청에는 인증 토큰이 포함될 수 있습니다. 사용자 이름/암호 인증을 사용한 경우 요청에 `AuthenticationToken` 생성된 사람 `AuthenticationHandler`를 입력하면 SDK는 라이선스를 발급하기 전에 토큰이 유효한지 확인합니다.
