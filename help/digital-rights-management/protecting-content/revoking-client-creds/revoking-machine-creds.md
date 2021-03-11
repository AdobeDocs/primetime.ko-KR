---
title: 컴퓨터 자격 증명을 취소하는 중
description: 컴퓨터 자격 증명을 취소하는 중
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# 컴퓨터 자격 증명을 취소하는 중 {#revoking-machine-credentials}

Adobe은 손상된 것으로 알려진 시스템 자격 증명을 취소하기 위해 CRL을 유지합니다. 이 CRL은 SDK에 의해 자동으로 적용됩니다. 라이선스 서버에서 라이선스를 발급하지 않으려는 추가 컴퓨터가 있는 경우 컴퓨터 해지 목록을 만들고 제외할 컴퓨터 토큰의 발급자 이름과 일련 번호를 추가할 수 있습니다(시스템 인증서의 발급자 이름 및 일련 번호를 검색하려면 `MachineToken.getMachineTokenId()` 사용).

컴퓨터 자격 증명을 취소하는 경우에는 `RevocationListFactory` 개체 사용이 포함됩니다. 해지 목록을 만들려면 기존 해지 목록을 로드하고 Java API를 사용하여 컴퓨터 토큰이 해지되었는지 확인하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내에 [개발 환경 설정](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)에 언급된 모든 JAR 파일을 포함합니다.
1. 서명에 필요한 자격 증명을 로드할 `ServerCredentialFactory` 인스턴스를 만듭니다. 라이선스 서버 자격 증명은 해지 목록에 서명하는 데 사용됩니다.
1. `RevocationListFactory` 인스턴스를 만듭니다.
1. `IssuerAndSerialNumber` 개체를 사용하여 해지할 컴퓨터 토큰의 발급자 및 일련 번호를 지정합니다. 모든 Adobe Primetime DRM 요청에 컴퓨터 토큰이 포함되어 있습니다.
1. 방금 만든 `IssuerAndSerialNumber` 개체를 사용하여 `RevocationList` 개체를 만들고 `RevocationListFactory.addRevocationEntry()`에 전달하여 해지 목록에 추가합니다. `RevocationListFactory.generateRevocationList()`을(를) 호출하여 새 해지 목록을 생성합니다.

1. 해지 목록을 저장하려면 `RevocationList.getBytes()`을(를) 호출하여 정리 목록을 정리하십시오. 목록을 로드하려면 `RevocationListFactory.loadRevocationList()`을(를) 호출하고 직렬화된 목록을 전달합니다.

1. 서명이 유효하고 목록이 올바른 라이선스 서버에서 `RevocationList.verifySignature()`을(를) 호출하여 서명되었는지 확인합니다.
1. 항목이 취소되었는지 확인하려면 `IssuerAndSerialNumber` 개체를 `RevocationList.isRevoked()`에 전달합니다. 또한 해지 목록을 `HandlerConfiguration`에 전달하여 SDK가 모든 인증 및 라이센스 요청에 대해 해지 목록을 강제 적용할 수 있습니다.

기존 `RevocationList`에 항목을 더 추가하려면 기존 해지 목록을 로드합니다. 새 `RevocationListFactory` 인스턴스를 만들고 CRL 번호를 증가시켜야 합니다. 이전 목록의 모든 항목을 새 목록에 추가하려면 `RevocationListFactioryEntries.addRevocationEntries`을(를) 호출합니다. `RevocationListFactory.addRevocationEntry`을(를) 호출하여 RevocationList에 새 해지 항목을 추가합니다.

해지 목록을 만들고, 기존 해지 목록을 로드하고, 컴퓨터 토큰이 해지되었는지 확인하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 [!DNL samples] 디렉토리의 `com.adobe.flashaccess.samples.revocation.CreateRevocationList`을 참조하십시오.
