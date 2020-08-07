---
seo-title: 라이선스 사전 생성
title: 라이선스 사전 생성
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 라이선스 사전 생성{#pre-generating-licenses}

라이선스를 미리 생성하려면 를 사용하여 인스턴스 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 를 가져옵니다 `LicenseFactory`. 이 공장에서 생성된 라이선스에 서명하려면 라이센스 서버 자격 증명을 지정해야 합니다. 이 클래스는 고급 라이선스 체인으로 라이선스 체인 및 리프 및 루트 라이선스 없이 리프 라이선스 생성을 [지원합니다](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

리프 라이선스를 생성할 때 컨텐츠 메타데이터를 사용하여 지정해야 합니다 `initContentInfo()`. 메타데이터에 여러 정책이 포함되어 있거나 메타데이터에 포함되지 않은 정책을 사용하려는 경우 라이선스 생성 `setSelectedPolicy()` 에 사용할 정책을 지정합니다. 정책 업데이트 목록을 사용하여 정책 업데이트를 추적하는 경우 메타데이터를 사용하여 초기화하기 전에 라이센스 팩터리에 정책 업데이트 목록을 제공할 수 있습니다 `setPolicyUpdateList()`.

루트 라이센스를 생성할 때 컨텐츠 메타데이터는 위에 설명된 대로 지정될 수 있습니다. 또는 메타데이터 대신 정책() 및 라이센스 서버 URL()을 사용하여 루트 라이센스 `setSelectedPolicy()`를 생성할 수 `setLicenseServerURL()`있습니다.

>[!NOTE]
>
>클라이언트가 라이센스를 요청할 수 있는 Adobe 액세스 라이센스 서버가 없는 경우에도 라이센스 서버 URL이 필요합니다. 이 경우 라이선스 서버 URL은 라이선스 발급자를 식별하는 URL을 지정해야 합니다.

정책에서 고급 라이센스 체인을 사용하는 경우 정책()의 루트 암호화 키를 해독하려면 라이센스 서버 자격 증명을 지정해야 합니다. `setRootKeyRetrievalInfo()`

정책에 도메인 바인딩된 라이센스가 필요한 경우 라이센스 서버 `setDomainCAs()` 가 도메인 토큰을 수락할 도메인 발급자를 지정하는 데 사용합니다. 라이선스 수신자의 유효성을 검사하려면 하나 이상의 도메인 CA 인증서를 제공해야 합니다.

정책에서 iOS 장치에 대한 원격 키 배달을 필요로 하는 경우, 체인화된 Leaf가 생성되지 않는 한 키 서버 인증서를 사용하여 제공해야 `setKeyServerCertificate()`합니다.

라이센스를 생성하려면 라이센스 유형 `generateLicense()` (리프 또는 루트)과 하나 이상의 수신자 인증서를 불러와서 지정합니다. 받는 사람 인증서는 정책에 지정된 요구 사항에 따라 컴퓨터 인증서 또는 도메인 인증서가 됩니다. 체인 리프를 생성하는 경우 수신자가 필요하지 않습니다. 라이센스가 생성된 후 정책에 지정된 사용 규칙을 무시할 수 있습니다. 마지막으로, 호출 `signLicense()` 을 호출하여 라이센스에 서명하고 의 인스턴스를 가져옵니다 `PreGeneratedLicense`. 이제 라이센스를 파일에 저장(일련 번호가 할당된 라이센스를 검색하는 데 사용) `getBytes()` 하거나 암호화된 내용에 포함시킬 수 있습니다. 라이센스 [임베드 를 참조하십시오](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

사전 생성된 라이선스를 시연하는 샘플 코드는 참조 구현 명령줄 도구 &quot;샘플&quot; 디렉토리 `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 에서 참조하십시오.
