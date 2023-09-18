---
title: 도메인 등록 취소 요청 처리
description: 도메인 등록 취소 요청 처리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 도메인 등록 취소 요청 처리{#handling-domain-de-registration-requests}

클라이언트 애플리케이션이 도메인을 남겨야 하는 경우 `DRMManager.removeFromDeviceGroup()`ActionScript API 또는 `leaveLicenseDomain()` 도메인 등록 취소 프로세스를 시작하는 iOS API입니다. 도메인 등록 취소는 2단계 프로세스입니다. 클라이언트가 먼저 등록 취소 미리 보기 요청을 보냅니다. 도메인 서버는 요청을 검사하고 클라이언트가 도메인을 떠나도록 허용되는지 여부를 결정합니다(시스템이 현재 도메인에 속하지 않은 경우 오류가 반환될 수 있음). 응답이 성공하면 클라이언트는 도메인 자격 증명과 해당 도메인에 발급된 라이선스를 삭제한 다음 등록 취소 요청을 보냅니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 도메인 서버 URL: + &quot;/flashaccess/dereg/v4&quot;입니다. 그렇지 않은 경우, 요청 URL은 &quot;metadata&quot; + &quot;/flashaccess/dereg/v3&quot;의 도메인 서버 URL입니다.

도메인 등록 해제 요청을 처리할 때 서버는 `getRequestPhase()` 클라이언트가 미리보기 또는 등록 취소 단계에 있는지 여부를 확인합니다. 미리보기 단계에서 도메인 서버는 요청을 검사하고 클라이언트가 도메인을 떠나도록 허용되는지 여부를 결정합니다(예: 시스템이 현재 도메인에 속하지 않은 경우 요청이 거부될 수 있음). 등록 취소 단계에서 서버는 시스템이 도메인을 떠났다는 사실을 기록합니다. 서버는 두 번째 단계가 실패할 가능성을 최소화하기 위해 실제 등록 취소 요청과 동일한 논리를 미리 보기 요청에서 평가하는 것이 좋습니다.
