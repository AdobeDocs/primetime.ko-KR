---
seo-title: 도메인 등록 요청 처리
title: 도메인 등록 요청 처리
uuid: d92db6c2-5a16-41ea-a1aa-541c59780678
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# 도메인 등록 요청 처리 {#handle-domain-registration-requests}

DRM 메타데이터가 컨텐츠를 재생하는 데 도메인 등록이 필요하다고 표시되는 경우 클라이언트 응용 프로그램은 `DRMManager.addToDeviceGroup()` ActionScript API 또는 `joinLicenseDomain()` iOS API를 불러와야 합니다. 클라이언트가 지정된 도메인 서버에 아직 등록하지 않은 경우(또는 응용 프로그램이 다시 가입해야 하는 경우) 도메인 등록 요청이 전송됩니다. 도메인 서버는 클라이언트가 도메인에 가입할 수 있는지 여부를 확인하고 클라이언트에 하나 이상의 도메인 자격 증명을 발행합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`입니다.
* 클라이언트와 서버 지원 프로토콜 버전 5가 모두 있는 경우 요청 URL은 &quot;메타데이터의 도메인 서버 URL:+ &quot; [!DNL /flashaccess/domain/v4]&quot;. 그렇지 않으면 요청 URL이 메타데이터&quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;의 도메인 서버 URL입니다.

`DomainRegistrationHandler`을(를) 시작할 때 도메인 서버 URL을 지정해야 합니다. 그런 다음 이 URL은 토큰이 발급된 도메인 서버에 나타내기 위해 처리기가 발행한 도메인 토큰에 포함됩니다. URL은 서버에 도메인 등록이 필요한 DRM 정책에 지정된 도메인 서버 URL과 일치해야 합니다.

클라이언트가 도메인에 가입할 수 있는지 여부를 확인하기 위해 서버는 요청에서 컴퓨터 및 사용자 정보를 검사할 수 있습니다. 서버가 클라이언트가 참여할 수 있는 도메인을 결정할 수도 있습니다.

>[!NOTE]
>
>클라이언트는 도메인 서버 URL당 하나의 도메인의 구성원만 될 수 있습니다. 컴퓨터에 이 도메인 서버 URL에 대한 도메인 토큰이 이미 있는 경우 도메인 등록 요청에는 현재 도메인 이름( `getRequestDomainName()`)이 포함됩니다.

다시 가입 요청의 경우 도메인 서버는 이 도메인에 대한 현재 도메인 자격 증명 집합을 반환하거나 오류를 반환해야 합니다. 도메인 서버는 다른 도메인에 대한 도메인 자격 증명을 반환하지 않을 수 있습니다.

도메인에 가입하는 컴퓨터를 식별하고 카운트하는 방법에 대한 자세한 내용은 [컴퓨터 식별자 사용](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers)을 참조하십시오.

도메인 서버에 도메인에 가입하기 위한 인증이 필요한 경우 요청에 인증 토큰이 포함되어야 합니다. 라이센스 요청과 마찬가지로 도메인 등록에도 사용자 이름/암호 또는 사용자 정의 인증이 필요할 수 있습니다.

인증 토큰을 관리하는 방법에 대한 자세한 내용은 [사용자 인증](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication)을 참조하십시오.

도메인 서버는 각 도메인에 연결된 도메인 키를 저장하고 관리하는 책임을 집니다. 도메인에 대해 새 키 쌍을 생성해야 하는 경우(도메인의 첫 번째 도메인 등록) `generateDomainCredential(String, int, Principal, Date)`을 호출해야 합니다. 이 메서드는 새 도메인 키 쌍 및 도메인 인증서를 생성합니다. 도메인 서버는 개인 키와 인증서를 저장하고 이 도메인에 대한 후속 요청을 처리할 때 해당 개체를 제공해야 합니다. 키 위에 롤오버하기 위해 도메인에 대한 새 키 쌍을 생성할 수도 있습니다. 특정 도메인에 대한 키 위에 롤오버할 때는 `generateDomainCredential`에서 키 버전을 하나씩 증가시켜야 합니다.

이후 컴퓨터가 동일한 도메인에 등록될 때마다 동일한 도메인 개인 키와 인증서를 사용해야 합니다. 기존 도메인 자격 증명을 클라이언트에 반환하려면 `addDomainCredential(DomainToken, PrivateKey)`을(를) 호출합니다. 도메인 키가 변경되었기 때문에 도메인에 대한 도메인 자격 증명이 여러 개 있는 경우 클라이언트가 이전 도메인 키에 바인딩된 라이센스를 사용할 수 있도록 서버가 현재 도메인 키와 모든 이전 도메인 키에 대한 도메인 자격 증명을 제공해야 합니다. 이렇게 하면 이전 도메인 토큰에 바인딩된 라이선스가 새로 등록된 컴퓨터로 이동되고 계속 재생할 수 있습니다.
