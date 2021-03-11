---
title: 정책 업데이트 목록 작업
description: 정책 업데이트 목록 작업
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# 정책 업데이트 목록 작업{#working-with-policy-update-lists}

정책에 대한 정보를 저장하기 위한 데이터베이스에 대한 액세스 권한이 없는 라이센스 서버의 경우, 정책 업데이트 목록을 사용하여 라이센스 서버에 업데이트된 정책을 알릴 수 있습니다. 정책 업데이트 목록에는 업데이트된 버전의 정책 또는 취소된 정책 ID 목록이 포함될 수 있습니다. 정책 업데이트 목록이 `HandlerConfiguration`에 제공되면 SDK에서 라이센스를 발급할 때 이 목록을 적용합니다.

컨텐트 소유자 또는 배포자가 특정 정책에 따라 라이센스 발행을 중단하려는 경우에도 정책이 취소될 수 있습니다. 정책 업데이트 목록은 SDK에서 정책 취소를 적용하는 데 사용할 수 있습니다. 정책 업데이트 목록은 SDK에 업데이트된 정책 목록을 제공하는 데에도 사용할 수 있습니다. 정책을 취소하면 이미 발급된 라이선스가 취소되지 않습니다. 해당 정책에 따라 추가 라이선스가 발급되지 못하도록 합니다.

정책 업데이트 목록 작업에는 `PolicyUpdateListFactory` 개체 사용이 포함됩니다. 정책 업데이트 목록을 만들고, 기존 정책 업데이트 목록을 로드하고, Java API를 사용하여 정책이 업데이트되었는지 또는 폐지되었는지 확인하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 설정에 설명된 모든 JAR 파일을 포함합니다.
1. 서명에 필요한 자격 증명을 로드할 `ServerCredentialFactory` 인스턴스를 만듭니다.
1. 만든 `ServerCredential`을(를) 사용하여 `PolicyUpdateListFactory` 인스턴스를 만듭니다.
1. 해지할 정책 ID를 지정합니다.
1. 방금 만든 정책 ID `String`을 사용하여 `PolicyRevocationEntry` 개체를 만들고 `PolicyUpdateListFactory.addRevocationEntry()`에 전달하여 정책 업데이트 목록에 추가합니다. `PolicyUpdateListFactory.generatePolicyUpdateList()`을(를) 호출하여 새 정책 업데이트 목록을 생성합니다. 마찬가지로 업데이트된 정책을 `PolicyUpdateEntry`을 사용하여 목록에 추가할 수 있습니다.
1. 정책 업데이트 목록이 이미 있는 경우 `PolicyUpdateList.getBytes()`을(를) 호출하여 로드할 목적으로 일련 번호를 등록할 수 있습니다. 목록을 로드하려면 `PolicyUpdateListFactory.loadPolicyUpdateList()`을(를) 호출하고 직렬화된 목록을 전달합니다.
1. 서명이 유효하고 `PolicyUpdateList.verifySignature()`을(를) 호출하여 올바른 라이센스 서버 인증서에 의해 목록이 서명되었는지 확인합니다.
1. 항목이 취소되었는지 확인하려면 정책 ID `String`을(를) `PolicyUpdateList.isRevoked()`에 전달합니다. 또는 목록을 `HandlerConfiguration`으로 전달할 수 있으며 라이선스를 발행할 때 적용됩니다.

기존 `PolicyUpdateList`에 항목을 더 추가하려면 기존 정책 업데이트 목록을 로드합니다. 새 `PolicyUpdateListFactory` 인스턴스를 만듭니다. 이전 목록의 모든 항목을 새 목록에 추가하려면 P `olicyUpdateListFactory.addEntries`을(를) 호출합니다. PolicyUpdateList에 새 해지 또는 업데이트 항목을 추가하려면 `PolicyUpdateListFactory.addRevocationEntry` 또는 `addUpdatedEntry`을(를) 호출하십시오.

정책 업데이트 목록을 만들고, 기존 정책 업데이트 목록을 로드하고, 정책이 폐지되었는지 확인하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리의 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList`을 참조하십시오.
