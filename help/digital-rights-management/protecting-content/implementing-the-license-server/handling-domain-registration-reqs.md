---
title: 도메인 등록 요청 처리
description: 도메인 등록 요청 처리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 도메인 등록 요청 처리 {#handle-domain-registration-requests}

DRM 메타데이터가 콘텐츠를 재생하기 위해 도메인 등록이 필요함을 나타내는 경우 클라이언트 애플리케이션은 `DRMManager.addToDeviceGroup()` ActionScript API 또는 `joinLicenseDomain()` iOS API. 클라이언트가 지정된 도메인 서버에 아직 등록되지 않은 경우(또는 애플리케이션이 강제로 다시 가입하는 경우) 도메인 등록 요청이 전송됩니다. 도메인 서버는 클라이언트가 도메인에 가입할 수 있는지 여부를 결정하고 클라이언트에 하나 이상의 도메인 자격 증명을 발급합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* 클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 도메인 서버 URL: + &quot; [!DNL /flashaccess/domain/v4]&quot;. 그렇지 않으면 요청 URL은 메타데이터의 도메인 서버 URL&quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

을(를) 초기화할 때 `DomainRegistrationHandler`도메인 서버 URL을 지정해야 합니다. 그런 다음 이 URL은 핸들러가 발급한 도메인 토큰에 포함되어 도메인 서버에 토큰이 발급되었음을 나타냅니다. URL은 서버에 도메인 등록이 필요한 DRM 정책에 지정된 도메인 서버 URL과 일치해야 합니다.

클라이언트가 도메인에 가입하는 것이 허용되는지 여부를 결정하기 위해, 서버는 요청에서 기계 및 사용자 정보를 검사할 수 있다. 서버는 또한 클라이언트가 가입하도록 허용된 도메인을 결정할 수 있다.

>[!NOTE]
>
>클라이언트는 도메인 서버 URL당 하나의 도메인에 속한 구성원만 될 수 있습니다. 컴퓨터에 이미 이 도메인 서버 URL에 대한 도메인 토큰이 있는 경우 도메인 등록 요청에 현재 도메인 이름( `getRequestDomainName()`).

재가입 요청의 경우 도메인 서버는 이 도메인에 대한 현재 도메인 자격 증명 집합을 반환하거나 오류를 반환해야 합니다. 도메인 서버가 다른 도메인에 대한 도메인 자격 증명을 반환하지 않을 수 있습니다.

다음을 참조하십시오 [머신 식별자 사용](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) 도메인에 가입하는 시스템을 식별하고 카운트하는 방법에 대한 정보입니다.

도메인 서버가 도메인에 가입하기 위해 인증을 필요로 하는 경우 요청에 인증 토큰이 포함되어야 합니다. 라이선스 요청과 마찬가지로 도메인 등록에도 사용자 이름/암호 또는 사용자 지정 인증이 필요할 수 있습니다.

다음을 참조하십시오 [사용자 인증](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) 인증 토큰 관리 방법에 대한 자세한 내용을 보려면 여기를 클릭하십시오.

도메인 서버는 각 도메인과 연관된 도메인 키를 저장하고 관리합니다. 도메인(도메인에 대한 첫 번째 도메인 등록)에 대해 새 키 쌍을 생성해야 하는 경우 을 호출해야 합니다 `generateDomainCredential(String, int, Principal, Date)`. 이 메서드는 새 도메인 키 쌍과 도메인 인증서를 생성합니다. 도메인 서버는 이 도메인에 대한 후속 요청을 처리할 때 개인 키와 인증서를 저장하고 해당 개체를 제공해야 합니다. 키를 롤오버하기 위해 도메인에 대한 새 키 쌍을 생성할 수도 있습니다. 특정 도메인에 대한 키를 롤오버할 때에서 키 버전을 늘려야 합니다. `generateDomainCredential`.

컴퓨터가 동일한 도메인에 등록할 때마다 동일한 도메인 개인 키와 인증서를 사용해야 합니다. 호출 `addDomainCredential(DomainToken, PrivateKey)` 기존 도메인 자격 증명을 클라이언트에 반환합니다. 도메인 키가 변경되었기 때문에 도메인에 대한 도메인 자격 증명이 여러 개 있는 경우 서버는 현재 도메인 키와 모든 이전 도메인 키에 대한 도메인 자격 증명을 제공해야 클라이언트가 이전 도메인 키에 바인딩된 라이선스를 사용할 수 있습니다. 이렇게 하면 이전 도메인 토큰에 바인딩된 라이선스를 새로 등록된 컴퓨터로 이동하여 계속 재생할 수 있습니다.
