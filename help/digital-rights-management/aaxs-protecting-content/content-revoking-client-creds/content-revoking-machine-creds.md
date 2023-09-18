---
title: 컴퓨터 자격 증명 취소
description: 컴퓨터 자격 증명 취소
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# 컴퓨터 자격 증명 취소{#revoking-machine-credentials}

Adobe은 손상된 것으로 알려진 컴퓨터 자격 증명을 취소하기 위한 CRL을 유지 관리합니다. 이 CRL은 SDK에 의해 자동으로 적용됩니다. 라이선스 서버에서 라이선스를 발급하지 않으려는 추가 컴퓨터가 있는 경우 컴퓨터 해지 목록을 만들고 제외하려는 컴퓨터 토큰의 발급자 이름 및 일련 번호를 추가할 수 있습니다(사용) `MachineToken.getMachineTokenId()` 컴퓨터 인증서의 발급자 이름 및 일련 번호를 검색합니다.

컴퓨터 자격 증명 취소에는 `RevocationListFactory` 개체. 해지 목록을 만들고 기존 해지 목록을 로드한 다음 Java API를 사용하여 컴퓨터 토큰이 해지되었는지 확인하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고에 언급된 모든 JAR 파일을 포함하십시오. [개발 환경 설정](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 을 참조하십시오.
1. 만들기 `ServerCredentialFactory` 서명에 필요한 자격 증명을 로드할 인스턴스입니다. 라이선스 서버 자격 증명은 해지 목록에 서명하는 데 사용됩니다.
1. 만들기 `RevocationListFactory` 인스턴스.
1. 다음을 사용하여 해지할 컴퓨터 토큰의 발급자 및 일련 번호를 지정하십시오. `IssuerAndSerialNumber` 개체. 모든 Adobe 액세스 요청에 컴퓨터 토큰이 포함됩니다.
1. 만들기 `RevocationList` 을 사용하는 개체 `IssuerAndSerialNumber` 방금 만든 개체를 해지 목록에 추가합니다. `RevocationListFactory.addRevocationEntry()`. 를 호출하여 새 해지 목록 생성 `RevocationListFactory.generateRevocationList()`.
1. 해지 목록을 저장하려면 를 호출하여 직렬화할 수 있습니다. `RevocationList.getBytes()`. 목록을 로드하려면 을 호출하십시오. `RevocationListFactory.loadRevocationList()` serialize된 목록을 전달합니다.
1. 를 호출하여 서명이 유효하고 목록이 올바른 라이선스 서버에 의해 서명되었는지 확인하십시오. `RevocationList.verifySignature()`.
1. 항목이 취소되었는지 확인하려면 `IssuerAndSerialNumber` 에 오브젝트 추가 `RevocationList.isRevoked()`. 해지 목록은에 전달될 수도 있습니다. `HandlerConfiguration` SDK가 모든 인증 및 라이선스 요청에 대해 해지 목록을 적용하도록 합니다.

기존 항목에 추가 항목 추가하기 `RevocationList`기존 해지 목록을 로드합니다. 새로 만들기 `RevocationListFactory` CRL 번호를 증가시키십시오. 호출 `RevocationListFactioryEntries.addRevocationEntries` 이전 목록의 모든 항목을 새 목록에 추가합니다. 호출 `RevocationListFactory.addRevocationEntry` RevocationList에 새 해지 항목을 추가합니다.

해지 목록을 만들고 기존 해지 목록을 로드하며 컴퓨터 토큰이 해지되었는지 여부를 확인하는 방법을 보여 주는 샘플 코드는 을 참조하십시오. `com.adobe.flashaccess.samples.revocation.CreateRevocationList` 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리에서
