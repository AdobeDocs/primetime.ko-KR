---
title: 정책 업데이트 목록 작업
description: 정책 업데이트 목록 작업
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# 정책 업데이트 목록 작업{#working-with-policy-update-lists}

정책에 대한 정보를 저장하는 데이터베이스에 액세스할 수 없는 라이센스 서버의 경우 정책 업데이트 목록을 사용하여 라이센스 서버에 업데이트된 정책을 알릴 수 있습니다. 정책 업데이트 목록에는 취소된 정책의 업데이트된 버전이나 정책 ID 목록이 포함될 수 있습니다. 정책 업데이트 목록이 제공된 경우 `HandlerConfiguration`, SDK는 라이센스를 발급할 때 이 목록을 적용합니다.

콘텐츠 소유자 또는 배포자가 특정 정책에 따라 라이선스 발급을 중단하려는 경우 정책이 취소될 수도 있습니다. 정책 업데이트 목록을 사용하여 SDK에서 정책을 해지할 수 있습니다. 정책 업데이트 목록은 SDK에 업데이트된 정책 목록을 제공하는 데 사용할 수도 있습니다. 정책을 취소해도 이미 발급된 라이선스는 취소되지 않습니다. 해당 정책에 따라 추가 라이선스를 발급할 수 없도록 할 뿐이다.

정책 업데이트 목록 작업에는 `PolicyUpdateListFactory` 개체. 정책 업데이트 목록을 만들고 기존 정책 업데이트 목록을 로드한 다음 Java API를 사용하여 정책이 업데이트되었는지 또는 취소되었는지 확인하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 설정에 언급된 모든 JAR 파일을 포함합니다.
1. 만들기 `ServerCredentialFactory` 서명에 필요한 자격 증명을 로드할 인스턴스입니다.
1. 만들기 `PolicyUpdateListFactory` 를 사용하는 인스턴스 `ServerCredential` 을(를) 만들었습니다.
1. 해지할 정책 ID를 지정하십시오.
1. 만들기 `PolicyRevocationEntry` 정책 ID를 사용하는 개체 `String` 방금 을(를) 만들었고, 이 파일을 (으)로 전달하여 정책 업데이트 목록에 추가했습니다. `PolicyUpdateListFactory.addRevocationEntry()`. 를 호출하여 새 정책 업데이트 목록 생성 `PolicyUpdateListFactory.generatePolicyUpdateList()`. 마찬가지로 업데이트된 정책은 를 사용하여 목록에 추가할 수 있습니다. `PolicyUpdateEntry`.
1. 정책 업데이트 목록이 이미 있는 경우 를 호출하여 로드할 수 있도록 직렬화할 수 있습니다. `PolicyUpdateList.getBytes()`. 목록을 로드하려면 을 호출하십시오. `PolicyUpdateListFactory.loadPolicyUpdateList()` serialize된 목록을 전달합니다.
1. 를 호출하여 서명이 유효하고 목록이 올바른 라이선스 서버 인증서에 의해 서명되었는지 확인하십시오. `PolicyUpdateList.verifySignature()`.
1. 항목이 취소되었는지 확인하려면 정책 ID를 전달합니다 `String` 대상 `PolicyUpdateList.isRevoked()`. 또는 목록을에 전달할 수 있습니다. `HandlerConfiguration` 그리고 그것은 면허증이 발급될 때 시행될 것입니다.

기존 항목에 추가 항목 추가하기 `PolicyUpdateList`기존 정책 업데이트 목록을 로드합니다. 새로 만들기 `PolicyUpdateListFactory` 인스턴스. 호출 P `olicyUpdateListFactory.addEntries` 이전 목록의 모든 항목을 새 목록에 추가합니다. 호출 `PolicyUpdateListFactory.addRevocationEntry` 또는 `addUpdatedEntry` PolicyUpdateList에 새 해지 또는 업데이트 항목을 추가합니다.

정책 업데이트 목록을 만들고 기존 정책 업데이트 목록을 로드하며 정책이 취소되었는지 확인하는 방법을 보여 주는 샘플 코드는 을 참조하십시오. `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리에서
