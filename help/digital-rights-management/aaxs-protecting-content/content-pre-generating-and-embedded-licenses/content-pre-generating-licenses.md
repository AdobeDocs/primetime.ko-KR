---
title: 라이선스 사전 생성 중
description: 라이선스 사전 생성 중
copied-description: true
exl-id: 2be8674c-736f-4ed3-b952-f661bf3ff48f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 라이선스 사전 생성 중{#pre-generating-licenses}

라이센스를 미리 생성하려면 다음을 사용합니다 `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` 의 인스턴스를 획득하려면 `LicenseFactory`. 이 공장에서 생성한 라이선스를 서명하려면 라이선스 서버 자격 증명을 지정해야 합니다. 이 클래스는 라이센스 체인이 없는 리프 라이센스 생성 및 를 사용한 리프 및 루트 라이센스 생성을 지원합니다. [향상된 라이선스 체인](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Leaf 라이선스를 생성할 때 컨텐츠 메타데이터는 다음을 사용하여 지정해야 합니다. `initContentInfo()`. 메타데이터에 여러 정책이 포함되어 있거나 메타데이터에 없는 정책을 사용하려는 경우 `setSelectedPolicy()` 라이센스 생성에 사용할 정책을 지정합니다. 정책 업데이트 목록을 사용하여 정책에 대한 업데이트를 추적하는 경우 다음을 사용하여 메타데이터를 초기화하기 전에 라이선스 팩토리에 정책 업데이트 목록을 제공할 수 있습니다. `setPolicyUpdateList()`.

루트 라이센스를 생성할 때, 콘텐츠 메타데이터는 전술한 바와 같이 지정될 수 있다. 또는 정책( )을 사용하여 루트 라이센스를 생성할 수 있습니다. `setSelectedPolicy()`) 및 라이선스 서버 URL( `setLicenseServerURL()`)을 클릭하여 제품에서 사용할 수 있습니다.

>[!NOTE]
>
>클라이언트가 라이선스를 요청할 수 있는 Adobe 액세스 라이선스 서버가 없는 경우에도 라이선스 서버 URL이 필요합니다. 이 경우 라이선스 서버 URL은 라이선스 발급자를 식별하는 URL을 지정해야 합니다.

정책에 향상된 라이선스 체인이 사용되는 경우 정책의 루트 암호화 키를 해독하려면 라이선스 서버 자격 증명을 지정해야 합니다( `setRootKeyRetrievalInfo()`).

정책에 도메인 바인딩 라이선스가 필요한 경우 다음을 사용하십시오. `setDomainCAs()` 라이선스 서버가 도메인 토큰을 수락할 도메인 발급자를 지정합니다. 라이선스 수신자의 유효성을 검사하려면 하나 이상의 도메인 CA 인증서를 제공해야 합니다.

정책에 iOS 장치에 대한 원격 키 전달이 필요한 경우 다음을 사용하여 키 서버 인증서를 제공해야 합니다. `setKeyServerCertificate()`체인 리프가 생성되지 않는 경우.

라이선스를 생성하려면 를 호출하십시오. `generateLicense()` 라이선스 유형(리프 또는 루트)과 하나 이상의 수신자 인증서를 지정합니다. 정책에 지정된 요구 사항에 따라 수신자 인증서는 컴퓨터 인증서 또는 도메인 인증서가 됩니다. 체인 리프를 생성하는 경우 수신자가 필요하지 않습니다. 라이센스가 생성되면 정책에 지정된 사용 규칙을 재정의할 수 있습니다. 마지막으로 를 호출합니다 `signLicense()` 라이센스에 서명하고 의 인스턴스를 획득하려면 `PreGeneratedLicense`. 이제 라이센스를 파일에 저장할 수 있습니다(사용 `getBytes()` 를 사용하여 serialize된 라이선스)나 암호화된 콘텐츠에 임베드된 라이선스를 가져올 수 있습니다. 다음을 참조하십시오. [라이선스 포함](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

사전 생성된 라이센스를 보여 주는 샘플 코드는 다음을 참조하십시오. `com.adobe.flashaccess.samples.licensegen.GenerateLicense` 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리에서
