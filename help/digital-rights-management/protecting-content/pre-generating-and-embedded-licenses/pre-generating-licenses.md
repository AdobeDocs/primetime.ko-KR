---
description: Adobe Primetime DRM Professional을 사용하는 경우 라이선스를 미리 생성하여 컨텐츠에 라이선스를 포함할 수 있습니다. 이 기능은 고급 라이선스 체인과 결합할 수 있으므로 리프 라이센스가 사전에 생성되어 컨텐츠에 포함되고 클라이언트는 라이센스 서버에서 루트 라이센스(컴퓨터 또는 도메인에 바인딩됨)를 요청할 수 있습니다. 또는 클라이언트 응용 프로그램은 장치가 서버에 사전 등록되고, 서버가 해당 장치에 바인딩되는 라이센스를 미리 생성하며 클라이언트가 간단한 HTTP 웹 서버에서 라이센스를 검색하는 워크플로우를 구현할 수 있습니다.
title: 사전 생성 라이선스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# 사전 생성 라이센스 {#pre-generating-licenses}

Adobe Primetime DRM Professional을 사용하는 경우 라이선스를 미리 생성하여 컨텐츠에 라이선스를 포함할 수 있습니다. 이 기능은 고급 라이선스 체인과 결합할 수 있으므로 리프 라이센스가 사전에 생성되어 컨텐츠에 포함되고 클라이언트는 라이센스 서버에서 루트 라이센스(컴퓨터 또는 도메인에 바인딩됨)를 요청할 수 있습니다. 또는 클라이언트 응용 프로그램은 장치가 서버에 사전 등록되고, 서버가 해당 장치에 바인딩되는 라이센스를 미리 생성하며 클라이언트가 간단한 HTTP 웹 서버에서 라이센스를 검색하는 워크플로우를 구현할 수 있습니다.

라이선스를 미리 생성하려면 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()`을(를) 사용하여 `LicenseFactory`의 인스턴스를 구해야 합니다. 이 팩터리에서 생성된 라이선스에 서명하려면 라이센스 서버 자격 증명을 지정해야 합니다. 이 클래스는 [향상된 라이선스 체인](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md)을 사용하여 라이선스 체인 및 리프 및 루트 라이선스 없이 리프 라이선스를 생성할 수 있습니다.

리프 라이센스를 생성할 때 `initContentInfo()`을(를) 적용하는 컨텐츠 메타데이터를 지정해야 합니다. 메타데이터에 여러 DRM 정책이 포함되어 있거나 메타데이터에 포함되지 않은 DRM 정책을 사용하려는 경우 `setSelectedPolicy()`을(를) 사용하여 라이선스를 생성하려면 DRM 정책을 지정해야 합니다. DRM 정책 업데이트 목록을 사용하여 DRM 정책 업데이트를 추적하는 경우 `setPolicyUpdateList()`으로 메타데이터를 초기화하기 전에 DRM 정책 업데이트 목록을 라이선스 팩터리에 제공할 수 있습니다.

루트 라이센스를 생성할 때 위에 설명된 대로 컨텐츠 메타데이터를 지정해야 합니다. 또는 메타데이터 대신 DRM 정책( `setSelectedPolicy()`)과 라이선스 서버 URL( `setLicenseServerURL()`)을 적용하여 루트 라이선스를 생성할 수 있습니다.

>[!NOTE]
>
>클라이언트가 라이센스를 요청할 수 있는 Adobe Primetime DRM 라이센스 서버가 없는 경우에도 라이센스 서버 URL이 필요합니다. 이 경우 라이선스 서버 URL은 라이선스 발급자를 식별하는 URL을 지정해야 합니다.

DRM 정책이 고급 라이선스 체인을 사용하는 경우 DRM 정책( `setRootKeyRetrievalInfo()`)에서 루트 암호화 키를 해독하려면 라이센스 서버 자격 증명을 지정해야 합니다.

DRM 정책에 도메인 바인딩된 라이센스가 필요한 경우 `setDomainCAs()`을 사용하여 라이선스 서버에서 도메인 토큰을 허용하는 도메인 발급자를 지정해야 합니다. 라이선스 수신자의 유효성을 검사하려면 하나 이상의 도메인 CA 인증서를 제공해야 합니다.

iOS 장치에 대해 DRM 정책을 사용하려면 연결된 리프가 생성되지 않는 한 `setKeyServerCertificate()`을(를) 적용하여 키 서버 인증서를 제공해야 합니다.

라이센스를 생성하려면 `generateLicense()`을(를) 호출하고 라이센스 유형(리프 또는 루트) 및 하나 이상의 수신자 인증서를 지정해야 합니다. 받는 사람 인증서는 DRM 정책에 지정된 요구 사항에 따라 컴퓨터 인증서 또는 도메인 인증서를 나타냅니다. 체인 리프를 생성하는 경우 수신자는 필요하지 않습니다. 라이선스가 생성되면 DRM 정책에 지정된 사용 규칙을 재정의할 수 있습니다. 마지막으로 `signLicense()`을 호출하여 라이선스를 서명하고 `PreGeneratedLicense` 인스턴스를 구해야 합니다. 이제 라이선스를 저장할 수 있습니다(일련 번호가 할당된 라이선스를 검색하거나 암호화된 내용에 포함하려면 `getBytes()` 사용).

[라이선스 포함](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md)을 참조하십시오.

사전 생성된 라이센스를 시연하는 방법에 대한 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리의 `com.adobe.flashaccess.samples.licensegen.GenerateLicense`을 참조하십시오.
