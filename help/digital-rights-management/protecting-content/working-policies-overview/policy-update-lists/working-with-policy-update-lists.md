---
title: DRM 정책 업데이트 목록 작업
description: DRM 정책 업데이트 목록 작업
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# DRM 정책 업데이트에는 {#drm-policy-update-lists} 목록이 표시됩니다.

콘텐츠를 패키지화한 후 DRM 정책의 사용 규칙을 업데이트하는 경우 업데이트된 DRM 정책을 사용하는 라이선스를 발급하려면 라이선스 서버가 최신 버전을 가지고 있어야 합니다. 이를 실현하는 한 가지 방법은 DRM 정책 업데이트 목록을 이용하는 것입니다.

DRM 정책 업데이트 목록은 업데이트되었거나 해지된 DRM 정책 목록이 포함된 파일로 표시됩니다. DRM 정책을 업데이트할 때마다 새 DRM 정책 업데이트 목록을 생성하여 정기적으로 목록을 모든 라이센스 서버에 푸시해야 합니다.

## DRM 정책 업데이트 목록 작업 {#working-with-drm-policy-update-lists}

DRM 정책에 대한 정보를 저장하기 위한 데이터베이스에 대한 액세스 권한이 없는 라이선스 서버의 경우 DRM 정책 업데이트 목록을 사용하여 라이선스 서버에 업데이트된 DRM 정책을 알릴 수 있습니다. DRM 정책 업데이트 목록에는 업데이트된 버전의 DRM 정책 또는 해지된 DRM 정책 ID 목록이 포함될 수 있습니다. 정책 업데이트 목록이 `HandlerConfiguration`에 포함되어 있는 경우 SDK는 라이선스를 발행할 때 이 목록을 적용합니다.

또한 컨텐츠 소유자 또는 배포업체가 특정 DRM 정책에 따라 라이선스 발행을 중단하려는 경우 DRM 정책을 취소할 수 있습니다. DRM 정책 업데이트 목록을 사용하여 SDK에서 DRM 정책 해지를 적용할 수 있습니다. DRM 정책 업데이트 목록을 적용하여 SDK에 업데이트된 DRM 정책 목록을 제공할 수도 있습니다.

>[!NOTE]
>
>DRM 정책을 취소할 때마다 이미 발급된 라이선스는 자동으로 해지되지 않습니다. 해당 DRM 정책에 따라 추가 라이선스가 발급되지 않도록 합니다.

## 정책 업데이트 목록 업데이트{#update-policy-update-lists}

DRM 정책 업데이트 목록 작업에는 `PolicyUpdateListFactory` 개체 사용이 포함됩니다. DRM 정책 업데이트 목록을 만들려면 기존 DRM 정책 업데이트 목록을 로드한 다음 Java API를 사용하여 DRM 정책이 업데이트되었는지 또는 해지되었는지 확인해야 합니다.

DRM 정책 업데이트 목록을 사용하여 작업하려면:

1. 개발 환경을 설정하고 프로젝트에서 개발 환경을 설정할 때 포함된 모든 JAR 파일을 포함합니다.
1. 서명을 위해 필요한 자격 증명을 로드할 `ServerCredentialFactory` 인스턴스를 만듭니다.
1. 만든 `ServerCredential`을(를) 사용하여 `PolicyUpdateListFactory` 인스턴스를 만듭니다.
1. 취소할 DRM 정책 ID를 지정합니다.
1. 방금 만든 DRM 정책 ID `String`을 사용하여 `PolicyRevocationEntry` 개체를 만든 다음 `PolicyUpdateListFactory.addRevocationEntry()`에 전달하여 DRM 정책 업데이트 목록에 추가합니다.
1. `PolicyUpdateListFactory.generatePolicyUpdateList()`을(를) 호출하여 새 DRM 정책 업데이트 목록을 생성합니다.

   마찬가지로 `PolicyUpdateEntry`을 사용하여 DRM 정책을 목록에 업데이트할 수 있습니다.
1. DRM 정책 업데이트 목록이 이미 있는 경우 `PolicyUpdateList.getBytes()`을(를) 호출하여 로드할 목적으로 직렬화할 수 있습니다.

   목록을 로드하려면 `PolicyUpdateListFactory.loadPolicyUpdateList()`을(를) 호출하고 일련 번호가 할당된 목록에 전달합니다.
1. 서명이 유효하고 목록이 올바른 라이선스 서버 인증서로 서명되었는지 확인하려면 `PolicyUpdateList.verifySignature()`을(를) 호출하십시오.
1. DRM 정책 ID `String`을(를) `PolicyUpdateList.isRevoked()`에 전달하여 항목이 해지되었는지 확인합니다.

   또는 목록을 `HandlerConfiguration`에 전달하면 라이센스가 발급될 때마다 이 목록을 적용할 수 있습니다.
기존 `PolicyUpdateList`에 항목을 더 추가하려면 기존 DRM 정책 업데이트 목록을 로드해야 합니다. 따라서 새 DRM `PolicyUpdateListFactory` 인스턴스를 만들어야 합니다. 이전 목록의 모든 항목을 새 목록에 추가하려면 `PolicyUpdateListFactory.addEntries`을(를) 호출합니다. DRM PolicyUpdateList에 새 해지 또는 업데이트 항목을 추가하려면 `PolicyUpdateListFactory.addRevocationEntry` 또는 `addUpdatedEntry`을(를) 호출하십시오.

DRM 정책 업데이트 목록을 만드는 방법을 보여 주는 샘플 코드는 *참조 구현 명령줄 도구* [!DNL samples] 디렉토리의 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList`을 참조하십시오.
