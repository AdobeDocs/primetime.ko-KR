---
seo-title: DRM 정책 업데이트 목록 작업
title: DRM 정책 업데이트 목록 작업
uuid: 41f89671-81c6-4d3d-ac31-9c2a1980517a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# DRM 정책 업데이트 목록 {#drm-policy-update-lists}

콘텐츠를 패키지한 후 DRM 정책에서 사용 규칙을 업데이트하는 경우 업데이트된 DRM 정책을 사용하는 라이선스를 발급하려면 라이선스 서버에 최신 버전이 있어야 합니다. 이를 실현하는 한 가지 방법은 DRM 정책 업데이트 목록을 이용하는 것입니다.

DRM 정책 업데이트 목록은 업데이트되거나 해지된 DRM 정책 목록이 포함된 파일로 표시됩니다. DRM 정책을 업데이트할 때마다 새 DRM 정책 업데이트 목록을 생성하고 정기적으로 목록을 모든 라이센스 서버에 푸시해야 합니다.

## DRM 정책 업데이트 목록 작업 {#working-with-drm-policy-update-lists}

DRM 정책에 대한 정보를 저장할 데이터베이스에 대한 액세스 권한이 없는 라이센스 서버의 경우 DRM 정책 업데이트 목록을 사용하여 업데이트된 DRM 정책을 라이선스 서버에 알릴 수 있습니다. DRM 정책 업데이트 목록에는 업데이트된 버전의 DRM 정책 또는 해지된 DRM 정책 ID 목록이 포함될 수 있습니다. 정책 업데이트 목록이 에 포함되어 `HandlerConfiguration`있는 경우, SDK는 라이센스를 발행할 때 이 목록을 적용합니다.

또한 컨텐츠 소유자 또는 배포업체가 특정 DRM 정책에 따라 라이선스 발행을 중단하려는 경우 DRM 정책을 취소할 수 있습니다. DRM 정책 업데이트 목록을 사용하여 SDK에서 DRM 정책 취소를 적용할 수 있습니다. DRM 정책 업데이트 목록을 적용하여 SDK에 업데이트된 DRM 정책 목록을 제공할 수도 있습니다.

>[!NOTE]
>
>DRM 정책을 취소할 때마다 이미 발급된 라이선스는 자동으로 취소되지 않습니다. 따라서 해당 DRM 정책에 따라 추가 라이선스가 발급되지 않습니다.

## 정책 업데이트 목록 업데이트{#update-policy-update-lists}

DRM 정책 업데이트 목록 작업에는 `PolicyUpdateListFactory` 개체 사용이 포함됩니다. DRM 정책 업데이트 목록을 만들려면 기존 DRM 정책 업데이트 목록을 로드한 다음 Java API를 사용하여 DRM 정책이 업데이트되었는지 또는 해지되었는지 확인해야 합니다.

DRM 정책 업데이트 목록을 사용하여 작업하려면

1. 개발 환경을 설정하고 프로젝트에서 개발 환경을 설정할 때 포함된 모든 JAR 파일을 포함합니다.
1. 서명을 위해 필요한 자격 증명을 로드할 `ServerCredentialFactory` 인스턴스를 만듭니다.
1. 만든 `PolicyUpdateListFactory` 인스턴스를 사용하여 `ServerCredential` 인스턴스를 만듭니다.
1. 취소할 DRM 정책 ID를 지정합니다.
1. 방금 만든 DRM 정책 ID `PolicyRevocationEntry` 를 사용하여 `String` 개체를 만든 다음 DRM 정책 업데이트 목록에 추가하여 만듭니다 `PolicyUpdateListFactory.addRevocationEntry()`.
1. 호출하여 새 DRM 정책 업데이트 목록을 생성합니다 `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   마찬가지로 를 사용하여 DRM 정책을 목록에 업데이트할 수 `PolicyUpdateEntry`있습니다.
1. DRM 정책 업데이트 목록이 이미 있는 경우 호출하여 로드하도록 직렬화할 수 `PolicyUpdateList.getBytes()`있습니다.

   목록을 불러오려면 `PolicyUpdateListFactory.loadPolicyUpdateList()` 호출한 후 직렬화된 목록에 전달합니다.
1. 서명이 유효한지, 올바른 라이센스 서버 인증서를 통해 목록에 서명되었는지 `PolicyUpdateList.verifySignature()`확인하십시오.
1. DRM 정책 ID를 `String` 에 전달하여 항목이 해지되었는지 `PolicyUpdateList.isRevoked()` 확인합니다.

   또는 라이선스를 발행할 때마다 목록이 `HandlerConfiguration` 적용되는 위치로 전달될 수 있습니다.
기존 항목에 항목을 더 추가하려면 기존 DRM 정책 업데이트 목록을 `PolicyUpdateList`로드해야 합니다. 따라서 새 DRM `PolicyUpdateListFactory` 인스턴스를 만들어야 합니다. 이전 목록의 모든 항목을 새 목록에 추가하려면 `PolicyUpdateListFactory.addEntries` 을 호출합니다. DRM PolicyUpdateList에 새 해지 또는 업데이트 항목을 추가하거나 `PolicyUpdateListFactory.addRevocationEntry` `addUpdatedEntry` 호출하십시오.

DRM 정책 업데이트 목록을 만드는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 `com.adobe.flashaccess.samples.policyupdatelist``.CreatePolicyUpdateList` 디렉토리에서 *을* 참조하십시오 [!DNL samples] .
