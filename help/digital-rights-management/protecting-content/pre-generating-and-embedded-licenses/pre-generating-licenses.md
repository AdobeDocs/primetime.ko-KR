---
description: Adobe Primetime DRM Professional을 사용하는 경우 라이선스를 미리 생성하고 콘텐츠에 라이선스를 포함할 수 있습니다. 이 기능은 Enhanced License Chaining과 결합하여 Leaf 라이선스가 미리 생성되어 콘텐츠에 포함되고 클라이언트가 라이선스 서버에서 루트 라이선스(컴퓨터 또는 도메인에 바인딩됨)를 요청할 수 있습니다. 또는 클라이언트 응용 프로그램은 장치가 서버에 사전 등록되고, 서버가 해당 장치에 바인딩된 라이선스를 사전 생성하고, 클라이언트가 간단한 HTTP 웹 서버에서 해당 라이선스를 검색하는 워크플로우를 구현할 수 있습니다.
title: 라이선스 사전 생성 중
exl-id: 6ced7dde-b4bb-470d-bdae-3042f5577b67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 라이선스 사전 생성 중 {#pre-generating-licenses}

Adobe Primetime DRM Professional을 사용하는 경우 라이선스를 미리 생성하고 콘텐츠에 라이선스를 포함할 수 있습니다. 이 기능은 Enhanced License Chaining과 결합하여 Leaf 라이선스가 미리 생성되어 콘텐츠에 포함되고 클라이언트가 라이선스 서버에서 루트 라이선스(컴퓨터 또는 도메인에 바인딩됨)를 요청할 수 있습니다. 또는 클라이언트 응용 프로그램은 장치가 서버에 사전 등록되고, 서버가 해당 장치에 바인딩된 라이선스를 사전 생성하고, 클라이언트가 간단한 HTTP 웹 서버에서 해당 라이선스를 검색하는 워크플로우를 구현할 수 있습니다.

라이센스를 미리 생성하려면 다음을 사용해야 합니다. `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 의 인스턴스를 획득하려면 `LicenseFactory`. 이 공장에서 생성한 라이선스를 서명하려면 라이선스 서버 자격 증명을 지정해야 합니다. 이 클래스는 라이센스 체인이 없는 리프 라이센스 생성 및 를 사용한 리프 및 루트 라이센스 생성을 지원합니다. [향상된 라이선스 체인](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Leaf 라이선스를 생성할 때 적용되는 콘텐츠 메타데이터를 지정해야 합니다 `initContentInfo()`. 메타데이터에 여러 DRM 정책이 포함되어 있거나 메타데이터에 포함되지 않은 DRM 정책을 사용하려면 를 사용해야 합니다 `setSelectedPolicy()` 라이센스를 생성할 DRM 정책을 지정합니다. DRM 정책 업데이트 목록을 사용하여 DRM 정책에 대한 업데이트를 추적하는 경우 `setPolicyUpdateList()`.

루트 라이센스를 생성할 때는 위에서 설명한 대로 컨텐츠 메타데이터를 지정해야 합니다. 또는 DRM 정책( )을 적용하여 루트 라이센스를 생성할 수 있습니다 `setSelectedPolicy()`) 및 라이선스 서버 URL( `setLicenseServerURL()`) 대신 사용할 수 있습니다.

>[!NOTE]
>
>클라이언트가 라이선스를 요청할 수 있는 Adobe Primetime DRM 라이선스 서버가 없는 경우에도 라이선스 서버 URL이 필요합니다. 이 경우 라이선스 서버 URL은 라이선스 발급자를 식별하는 URL을 지정해야 합니다.

DRM 정책이 향상된 라이센스 체인을 사용하는 경우 DRM 정책의 루트 암호화 키를 해독하기 위해 라이센스 서버 자격 증명을 지정해야 합니다( `setRootKeyRetrievalInfo()`).

DRM 정책에 도메인 바인딩 라이센스가 필요한 경우 `setDomainCAs()` 라이선스 서버가 도메인 토큰을 수락하는 도메인 발급자를 지정합니다. 라이선스 수신자의 유효성을 검사하려면 하나 이상의 도메인 CA 인증서를 제공해야 합니다.

DRM 정책이 iOS 장치에 대한 원격 키 전달을 필요로 하는 경우 를 적용하여 키 서버 인증서를 제공해야 합니다 `setKeyServerCertificate()` 체인 리프가 생성되지 않는 경우.

라이센스를 생성하려면 를 호출해야 합니다. `generateLicense()` 라이선스 유형(리프 또는 루트)과 하나 이상의 수신자 인증서를 지정합니다. 수신자 인증서는 DRM 정책에 지정된 요구 사항에 따라 컴퓨터 인증서 또는 도메인 인증서를 나타냅니다. 체인 리프를 생성하는 경우 수신자가 필요하지 않습니다. 라이센스가 생성되면 DRM 정책에 지정된 사용 규칙을 재정의할 수 있습니다. 마지막으로 `signLicense()` 라이센스에 서명하고 의 인스턴스를 획득하려면 `PreGeneratedLicense`. 이제 라이선스를 저장할 수 있습니다(사용) `getBytes()` serialize된 라이선스 또는 암호화된 콘텐츠에 포함된 라이선스를 검색합니다.

다음을 참조하십시오 [라이선스 포함](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

다음을 참조하십시오 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 미리 생성된 라이센스를 보여 주는 방법에 대한 샘플 코드가 필요하면 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리에서 참조하십시오.
