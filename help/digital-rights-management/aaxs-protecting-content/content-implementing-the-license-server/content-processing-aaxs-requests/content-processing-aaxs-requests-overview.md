---
seo-title: 개요
title: 개요
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 개요{#overview}

요청을 처리하는 일반적인 방법은 핸들러를 만들고, 요청을 구문 분석하고, 응답 데이터 또는 오류 코드를 설정하고, 핸들러를 닫는 것입니다.

단일 요청/응답 상호 작용을 처리하는 데 사용되는 기본 클래스는 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`입니다. 클래스의 인스턴스는 `HandlerConfiguration` 처리기를 초기화하는 데 사용됩니다. `HandlerConfiguration` 전송 자격 증명, 타임스탬프 허용치, 정책 업데이트 목록 및 해지 목록을 포함한 서버 구성 정보를 저장합니다. 이 처리기는 요청 데이터를 읽고 요청을 `RequestMessageBase`의 인스턴스로 구문 분석합니다. 호출자는 요청에 있는 정보를 검사하고 오류를 반환할지 또는 성공적인 응답을 결정할 수 있습니다(의 하위 클래스는 응답 데이터를 설정하는 방법을 `RequestMessageBase` 제공합니다).

요청이 성공하면 응답 데이터를 설정합니다.그렇지 않으면 실패 시 `RequestMessageBase.setErrorData()` 호출할 수 있습니다. 항상 메서드를 호출하여 구현을 종료합니다( `close()` 문의 `close()` 블록에서 `finally` `try` 호출하는 것이 좋습니다.). 핸들러를 호출하는 `MessageHandlerBase` 방법의 예는 API 참조 설명서를 참조하십시오.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>HTTP 상태 코드 200(확인)은 처리기에서 처리하는 모든 요청에 응답하여 전송해야 합니다. 서버 오류로 인해 처리기를 만들 수 없는 경우 서버가 500(내부 서버 오류)과 같은 다른 상태 코드로 응답할 수 있습니다.

클라이언트는 패키징 시 지정된 라이센스 서버 URL을 라이센스 서버로 전송된 모든 요청에 대한 기본 URL로 사용합니다. 예를 들어, 서버 URL이 &quot;https://licenseserver.com/path&quot;<span></span>로 지정된 경우 클라이언트는 요청을 &quot;https://licenseserver.com/path/flashaccess/...&quot;<span></span>로 보냅니다. 각 요청 유형에 사용되는 특정 경로에 대한 자세한 내용은 다음 섹션을 참조하십시오. 라이센스 서버를 구현할 때는 서버가 각 요청 유형에 필요한 경로에 응답해야 합니다.

라이센스 요청에는 인증 토큰이 포함될 수 있습니다. 사용자 이름/암호 인증이 사용된 경우, 요청에 에서 `AuthenticationToken` 생성한 항목이 포함될 수 `AuthenticationHandler`있으며, SDK는 라이센스를 발급하기 전에 토큰이 유효한지 확인합니다.
