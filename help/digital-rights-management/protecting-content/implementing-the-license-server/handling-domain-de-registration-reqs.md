---
title: 도메인 등록 취소 요청 처리
description: 도메인 등록 취소 요청 처리
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 도메인 등록 취소 요청 처리 {#handle-domain-de-registration-requests}

클라이언트 응용 프로그램이 도메인을 종료해야 하는 경우 `DRMManager.removeFromDeviceGroup()`ActionScript API 또는 `leaveLicenseDomain()` iOS API를 호출하여 도메인 등록 취소 프로세스를 시작합니다. 도메인 등록 제거는 2단계 프로세스입니다. 클라이언트가 먼저 등록 취소 미리 보기 요청을 전송합니다. 도메인 서버는 요청을 검토하고 클라이언트가 도메인을 떠날 수 있는지 여부를 결정합니다. 컴퓨터가 현재 도메인에 속해 있지 않은 경우 오류가 반환됩니다. 응답이 성공하면 클라이언트는 도메인 자격 증명과 해당 도메인에 발급된 모든 라이센스를 삭제합니다. 그런 다음 등록 취소 요청을 전송합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`입니다.
* 클라이언트 및 서버 지원 프로토콜 버전 5가 모두 지원되는 경우 요청 URL은 &quot;메타데이터의 도메인 서버 URL:+ &quot; [!DNL /flashaccess/dereg/v4]&quot;. 그렇지 않은 경우 요청 URL은 메타데이터&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;의 도메인 서버 URL입니다.

도메인 등록 취소 요청을 처리할 때 서버는 `getRequestPhase()`을 사용하여 클라이언트가 미리 보기 또는 등록 취소 단계에 있는지 확인합니다. 미리 보기 단계에서 도메인 서버는 요청을 검토하고 요청이 거부될 수 있으므로 클라이언트가 도메인을 떠날 수 있는지 여부를 결정합니다.예를 들어 컴퓨터가 현재 도메인에 속해 있지 않은 경우 요청이 거부될 수 있습니다. 등록 취소 단계에서는 컴퓨터가 도메인을 떠났다는 사실을 기록합니다. 서버는 두 번째 단계 실패 가능성을 최소화하기 위해 실제 등록 취소 요청에서와 같이 미리 보기 요청에서 동일한 로직을 평가하는 것이 좋습니다.
