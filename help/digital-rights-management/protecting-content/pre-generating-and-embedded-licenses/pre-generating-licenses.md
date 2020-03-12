---
description: Adobe Primetime DRM Professional을 사용하는 경우 라이선스를 미리 생성하여 콘텐츠에 라이선스를 임베드할 수 있습니다. 이 기능은 리프 라이센스가 미리 생성되어 컨텐츠에 포함되고 클라이언트가 라이센스 서버에서 루트 라이센스(시스템 또는 도메인에 바인딩됨)를 요청할 수 있도록 고급 라이센스 체인과 결합될 수 있습니다. 또는 클라이언트 응용 프로그램이 장치가 서버에 사전 등록되고 서버가 해당 장치에 바인딩되는 라이센스를 미리 생성하며 클라이언트가 간단한 HTTP 웹 서버에서 라이센스를 검색하는 워크플로우를 구현할 수 있습니다.
seo-description: Adobe Primetime DRM Professional을 사용하는 경우 라이선스를 미리 생성하여 콘텐츠에 라이선스를 임베드할 수 있습니다. 이 기능은 리프 라이센스가 미리 생성되어 컨텐츠에 포함되고 클라이언트가 라이센스 서버에서 루트 라이센스(시스템 또는 도메인에 바인딩됨)를 요청할 수 있도록 고급 라이센스 체인과 결합될 수 있습니다. 또는 클라이언트 응용 프로그램이 장치가 서버에 사전 등록되고 서버가 해당 장치에 바인딩되는 라이센스를 미리 생성하며 클라이언트가 간단한 HTTP 웹 서버에서 라이센스를 검색하는 워크플로우를 구현할 수 있습니다.
seo-title: 사전 생성 라이선스
title: 사전 생성 라이선스
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 사전 생성 라이선스 {#pre-generating-licenses}

Adobe Primetime DRM Professional을 사용하는 경우 라이선스를 미리 생성하여 콘텐츠에 라이선스를 임베드할 수 있습니다. 이 기능은 리프 라이센스가 미리 생성되어 컨텐츠에 포함되고 클라이언트가 라이센스 서버에서 루트 라이센스(시스템 또는 도메인에 바인딩됨)를 요청할 수 있도록 고급 라이센스 체인과 결합될 수 있습니다. 또는 클라이언트 응용 프로그램이 장치가 서버에 사전 등록되고 서버가 해당 장치에 바인딩되는 라이센스를 미리 생성하며 클라이언트가 간단한 HTTP 웹 서버에서 라이센스를 검색하는 워크플로우를 구현할 수 있습니다.

라이선스를 미리 생성하려는 경우 에 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 대한 인스턴스를 구해야 합니다 `LicenseFactory`. 이 팩터리에서 생성된 라이선스에 서명하려면 라이센스 서버 자격 증명을 지정해야 합니다. 이 클래스는 고급 라이선스 체인을 [](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md)통해 라이선스 체인 및 리프 및 루트 라이선스 없이 리프 라이선스를 생성할 수 있도록 지원합니다.

Leaf 라이선스를 생성할 때 적용되는 컨텐츠 메타데이터를 지정해야 합니다 `initContentInfo()`. 메타데이터에 여러 DRM 정책이 포함되어 있거나 메타데이터에 포함되지 않은 DRM 정책을 사용하려는 경우 DRM 정책을 `setSelectedPolicy()` 지정하여 라이선스를 생성해야 합니다. DRM 정책 업데이트 목록을 사용하여 DRM 정책 업데이트를 추적하는 경우 메타데이터를 초기화하기 전에 DRM 정책 업데이트 목록을 라이센스 팩터리에 제공할 수 `setPolicyUpdateList()`있습니다.

루트 라이센스를 생성할 때 위에 설명된 대로 컨텐츠 메타데이터를 지정해야 합니다. 또는 메타데이터 대신 DRM 정책() 및 라이센스 서버 URL( `setSelectedPolicy()``setLicenseServerURL()`)을 적용하여 루트 라이선스를 생성할 수 있습니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>클라이언트가 라이선스를 요청할 수 있는 Adobe Primetime DRM 라이선스 서버가 없는 경우에도 라이선스 서버 URL이 필요합니다. 이 경우 라이선스 서버 URL은 라이선스 발급자를 식별하는 URL을 지정해야 합니다.

DRM 정책이 고급 라이선스 체인을 사용하는 경우 DRM 정책( `setRootKeyRetrievalInfo()`)에서 루트 암호화 키를 해독하려면 라이센스 서버 자격 증명을 지정해야 합니다.

DRM 정책에 도메인 바인딩된 라이센스가 필요한 경우 라이센스 서버가 도메인 토큰을 수락하는 도메인 발급자를 `setDomainCAs()` 지정하는 데 사용해야 합니다. 라이선스 수신자의 유효성을 검사하려면 하나 이상의 도메인 CA 인증서를 제공해야 합니다.

DRM 정책에 iOS 장치에 대한 원격 키 전달이 필요한 경우 연결된 Leaf가 생성되지 `setKeyServerCertificate()` 않는 한 이를 적용하여 키 서버 인증서를 제공해야 합니다.

라이센스를 생성하려면 라이센스 유형(리프 또는 루트)과 하나 이상의 수신자 인증서를 불러와서 `generateLicense()` 지정해야 합니다. 받는 사람 인증서는 DRM 정책에 지정된 요구 사항에 따라 컴퓨터 인증서 또는 도메인 인증서를 나타냅니다. 체인으로 연결된 Leaf를 생성할 경우 수신자가 필요하지 않습니다. 라이센스가 생성된 후 DRM 정책에 지정된 사용 규칙을 무시할 수 있습니다. 마지막으로, 라이센스에 `signLicense()` 서명하고 인스턴스(인스턴스)를 얻기 위해 호출해야 `PreGeneratedLicense`합니다. 이제 라이선스를 저장할 수 있습니다(일련 번호가 할당된 라이선스를 `getBytes()` 검색하거나 암호화된 내용에 임베드할 때 사용).

라이선스 [임베딩을 참조하십시오](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

사전 생성된 라이선스를 시연하는 방법에 대한 샘플 코드는 참조 구현 명령줄 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 도구 &quot;샘플&quot; 디렉토리에서 을 참조하십시오.
