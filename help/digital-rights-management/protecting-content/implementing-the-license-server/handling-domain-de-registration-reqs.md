---
title: 도메인 등록 취소 요청 처리
description: 도메인 등록 취소 요청 처리
copied-description: true
exl-id: 14b97ba2-9344-4d84-8c52-f33126337454
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 도메인 등록 취소 요청 처리 {#handle-domain-de-registration-requests}

클라이언트 애플리케이션이 도메인을 남겨야 하는 경우 `DRMManager.removeFromDeviceGroup()`ActionScript API 또는 `leaveLicenseDomain()` 도메인 등록 취소 프로세스를 시작하는 iOS API입니다. 도메인 등록 취소는 2단계 프로세스입니다. 클라이언트가 먼저 등록 취소 미리 보기 요청을 보냅니다. 도메인 서버는 요청을 검사하고 클라이언트가 도메인을 떠나도록 허용되는지 여부를 결정합니다. 컴퓨터가 현재 도메인에 속해 있지 않으면 오류가 반환될 수 있습니다. 응답이 성공하면 클라이언트는 해당 도메인에 발급된 도메인 자격 증명과 모든 라이선스를 삭제합니다. 그런 다음 등록 취소 요청을 보냅니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 도메인 서버 URL: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. 그렇지 않으면 요청 URL은 메타데이터의 도메인 서버 URL&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

도메인 등록 해제 요청을 처리할 때 서버는 `getRequestPhase()` 클라이언트가 미리보기 또는 등록 취소 단계에 있는지 여부를 확인합니다. 미리보기 단계에서 도메인 서버는 요청을 검사하고 요청이 거부될 수 있으므로 클라이언트가 도메인을 떠나도록 허용되는지 여부를 결정합니다. 예를 들어 시스템이 현재 도메인의 일부가 아닌 경우 요청이 거부될 수 있습니다. 등록 취소 단계에서 서버는 시스템이 도메인을 떠났다는 사실을 기록합니다. 서버는 두 번째 단계가 실패할 가능성을 최소화하기 위해 실제 등록 취소 요청과 동일한 논리를 미리 보기 요청에서 평가하는 것이 좋습니다.
