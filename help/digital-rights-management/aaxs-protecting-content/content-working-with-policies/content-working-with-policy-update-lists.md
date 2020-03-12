---
seo-title: 정책 업데이트 목록 작업
title: 정책 업데이트 목록 작업
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 정책 업데이트 목록 작업{#working-with-policy-update-lists}

정책에 대한 정보를 저장하기 위한 데이터베이스에 대한 액세스 권한이 없는 라이센스 서버의 경우 정책 업데이트 목록을 사용하여 업데이트된 정책을 라이선스 서버에 알릴 수 있습니다. 정책 업데이트 목록에는 업데이트된 버전의 정책 또는 해지된 정책 ID 목록이 포함될 수 있습니다. 에 정책 업데이트 목록이 제공되면, SDK는 라이센스를 발급할 때 이 목록을 `HandlerConfiguration`적용합니다.

컨텐츠 소유자 또는 배포업체가 특정 정책에 따라 라이선스 발행을 중단하려는 경우에도 정책이 취소될 수 있습니다. 정책 업데이트 목록은 SDK에서 정책 취소를 적용하는 데 사용할 수 있습니다. 정책 업데이트 목록은 SDK에 업데이트된 정책 목록을 제공하는 데에도 사용할 수 있습니다. 정책을 취소하면 이미 발급된 라이선스가 취소되지 않습니다. 따라서 해당 정책에 따라 추가 라이선스가 발급되지 않습니다.

정책 업데이트 목록 작업에는 `PolicyUpdateListFactory` 개체 사용이 포함됩니다. 정책 업데이트 목록을 만들고, 기존 정책 업데이트 목록을 로드하고, Java API를 사용하여 정책이 업데이트되었는지 또는 해지되었는지 확인하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 설정에 언급된 모든 JAR 파일을 포함합니다.
1. 서명을 위해 필요한 자격 증명을 로드하는 `ServerCredentialFactory` 인스턴스를 만듭니다.
1. 만든 `PolicyUpdateListFactory` 인스턴스를 사용하여 `ServerCredential` 만듭니다.
1. 해지할 정책 ID를 지정합니다.
1. 방금 만든 정책 ID를 사용하여 `PolicyRevocationEntry` 개체를 `String` 만들고, 정책 업데이트 목록에 추가해서 추가합니다 `PolicyUpdateListFactory.addRevocationEntry()`. 호출을 통해 새 정책 업데이트 목록을 `PolicyUpdateListFactory.generatePolicyUpdateList()`생성합니다. 마찬가지로, 를 사용하여 업데이트된 정책을 목록에 추가할 수 `PolicyUpdateEntry`있습니다.
1. 정책 업데이트 목록이 이미 있는 경우 호출하여 로드하도록 직렬화할 수 `PolicyUpdateList.getBytes()`있습니다. 목록을 불러오려면 일련 `PolicyUpdateListFactory.loadPolicyUpdateList()` 목록을 호출하고 전달합니다.
1. 서명이 유효하고 목록을 올바른 라이선스 서버 인증서로 전화하여 서명했는지 `PolicyUpdateList.verifySignature()`확인합니다.
1. 항목이 취소되었는지 확인하려면 정책 ID를 `String` 에 `PolicyUpdateList.isRevoked()`전달합니다. 또는 목록을 전달하여 라이선스를 `HandlerConfiguration` 발행할 때 적용됩니다.

기존 정책에 항목을 더 추가하려면 기존 정책 업데이트 목록을 `PolicyUpdateList`로드합니다. 새 `PolicyUpdateListFactory` 인스턴스를 만듭니다. P `olicyUpdateListFactory.addEntries` 를 호출하여 이전 목록의 모든 항목을 새 목록에 추가합니다. PolicyUpdateList에 새 해지 또는 업데이트 항목을 추가하거나 `PolicyUpdateListFactory.addRevocationEntry` `addUpdatedEntry` 호출하십시오.

정책 업데이트 목록을 만들고, 기존 정책 업데이트 목록을 로드하고, 정책이 폐지되었는지 확인하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리에서 `com.adobe.flashaccess.samples.policyupdatelist` 을 참조하십시오 `.CreatePolicyUpdateList` .
