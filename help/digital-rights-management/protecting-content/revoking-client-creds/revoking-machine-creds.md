---
seo-title: 컴퓨터 자격 증명을 취소하는 중
title: 컴퓨터 자격 증명을 취소하는 중
uuid: 3647c843-5f1a-457e-949d-10a6278b1c29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 컴퓨터 자격 증명을 취소하는 중 {#revoking-machine-credentials}

Adobe는 컴퓨터 자격 증명이 손상된 것으로 알려진 것을 해지하기 위해 CRL을 유지합니다. 이 CRL 파섹 라이센스 서버에서 라이센스를 발급하지 않으려는 추가 컴퓨터가 있는 경우 시스템 해지 목록을 생성하고 제외할 컴퓨터 토큰의 발급자 이름과 일련 번호를 추가할 수 있습니다(시스템 인증서의 발급자 이름과 일련 번호를 검색하는 `MachineToken.getMachineTokenId()` 데 사용).

시스템 자격 증명을 취소하는 경우에는 `RevocationListFactory` 개체 사용이 포함됩니다. 해지 목록을 만들고, 기존 해지 목록을 로드하고, Java API를 사용하여 컴퓨터 토큰이 해지되었는지 확인하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 [설정에 언급된 모든 JAR 파일을](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) 포함합니다.
1. 서명을 위해 필요한 자격 증명을 로드하는 `ServerCredentialFactory` 인스턴스를 만듭니다. 라이선스 서버 자격 증명은 해지 목록에 서명하는 데 사용됩니다.
1. 인스턴스를 `RevocationListFactory` 만듭니다.
1. 개체를 사용하여 해지할 컴퓨터 토큰의 발급자 및 일련 번호를 `IssuerAndSerialNumber` 지정합니다. 모든 Adobe Primetime DRM 요청에는 컴퓨터 토큰이 포함되어 있습니다.
1. 방금 만든 개체를 사용하여 `RevocationList` 개체를 만들고, 이를 해지 목록에 추가하여 다시 `IssuerAndSerialNumber` `RevocationListFactory.addRevocationEntry()`만듭니다. 호출을 통해 새 해지 목록을 생성합니다 `RevocationListFactory.generateRevocationList()`.

1. 해지 목록을 저장하려면 전화하여 일련화할 수 `RevocationList.getBytes()`있습니다. 목록을 불러오려면 일련 `RevocationListFactory.loadRevocationList()` 목록을 호출하고 전달합니다.

1. 서명이 유효하고 목록이 올바른 라이선스 서버에서 전화하여 서명되었는지 `RevocationList.verifySignature()`확인합니다.
1. 항목이 취소되었는지 확인하려면 `IssuerAndSerialNumber` 개체를 `RevocationList.isRevoked()`로 전달합니다. 또한 SDK가 모든 인증 및 라이선스 요청에 대해 해지 목록을 `HandlerConfiguration` 적용하도록 해지 목록을 전달할 수 있습니다.

기존 항목에 항목을 더 추가하려면 기존 해지 목록을 `RevocationList`로드합니다. 새 `RevocationListFactory` 인스턴스를 만들고 CRL 번호를 늘립니다. 이전 목록의 모든 항목을 새 목록에 추가하려면 `RevocationListFactioryEntries.addRevocationEntries` 을 호출합니다. RevocationList에 새 해지 항목을 추가하려면 `RevocationListFactory.addRevocationEntry` 호출을 참조하십시오.

해지 목록을 만들고, 기존 해지 목록을 로드하고, 시스템 토큰이 폐지되었는지 확인하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 `com.adobe.flashaccess.samples.revocation.CreateRevocationList` [!DNL samples] 디렉토리에서 참조하십시오.
