---
title: DRM 정책 업데이트 목록 작업
description: DRM 정책 업데이트 목록 작업
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# DRM 정책 업데이트 목록 {#drm-policy-update-lists}

콘텐츠를 패키지한 후 DRM 정책에서 사용 규칙을 업데이트하는 경우 업데이트된 DRM 정책을 사용하는 라이선스를 발급하려면 라이선스 서버에 최신 버전이 있어야 합니다. DRM 정책 업데이트 목록을 통해 이를 수행할 수 있습니다.

DRM 정책 업데이트 목록은 업데이트되거나 취소된 DRM 정책 목록을 포함하는 파일로 표시됩니다. DRM 정책을 업데이트할 때마다 새 DRM 정책 업데이트 목록을 생성하고 이 목록을 모든 라이센스 서버에 정기적으로 푸시해야 합니다.

## DRM 정책 업데이트 목록 작업 {#working-with-drm-policy-update-lists}

DRM 정책에 대한 정보를 저장하는 데이터베이스에 액세스할 수 없는 라이센스 서버의 경우 DRM 정책 업데이트 목록을 사용하여 라이센스 서버에 업데이트된 DRM 정책을 알릴 수 있습니다. DRM 정책 업데이트 목록은 DRM 정책의 업데이트된 버전 또는 취소된 DRM 정책 ID 목록을 포함할 수 있습니다. 정책 업데이트 목록이에 포함된 경우 `HandlerConfiguration`, SDK는 라이선스를 발급할 때 이 목록을 적용합니다.

콘텐츠 소유자 또는 배포자가 특정 DRM 정책에 따라 라이선스 발급을 중단하려는 경우 DRM 정책을 취소할 수도 있습니다. DRM 정책 업데이트 목록을 사용하여 SDK에서 DRM 정책 취소를 적용할 수 있습니다. DRM 정책 업데이트 목록을 적용하여 업데이트된 DRM 정책 목록을 SDK에 제공할 수도 있습니다.

>[!NOTE]
>
>DRM 정책을 취소할 때마다 이미 발급된 라이센스는 자동으로 취소되지 않습니다. 해당 DRM 정책에 따라 추가 라이센스가 발행되지 않도록 할 뿐입니다.

## 정책 업데이트 목록 업데이트{#update-policy-update-lists}

DRM 정책 업데이트 목록 작업에는 `PolicyUpdateListFactory` 개체. DRM 정책 업데이트 목록을 만들려면 기존 DRM 정책 업데이트 목록을 로드한 다음 Java API를 사용하여 DRM 정책이 업데이트되었는지 취소되었는지 확인해야 합니다.

DRM 정책 업데이트 목록 작업하기

1. 개발 환경을 설정하고 프로젝트에서 개발 환경을 설정할 때 포함된 모든 JAR 파일을 포함합니다.
1. 만들기 `ServerCredentialFactory` 서명에 필요한 자격 증명을 로드할 인스턴스입니다.
1. 만들기 `PolicyUpdateListFactory` 를 사용한 인스턴스 `ServerCredential` 생성했습니다.
1. 취소할 DRM 정책 ID를 지정합니다.
1. 만들기 `PolicyRevocationEntry` drm 정책 ID를 사용하는 개체 `String` 방금 생성한 다음 DRM 정책 업데이트 목록에 추가하여 `PolicyUpdateListFactory.addRevocationEntry()`.
1. 를 호출하여 새 DRM 정책 업데이트 목록 생성 `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   마찬가지로 를 사용하여 DRM 정책을 목록에 업데이트할 수 있습니다 `PolicyUpdateEntry`.
1. DRM 정책 업데이트 목록이 이미 있는 경우 를 호출하여 로드하도록 직렬화할 수 있습니다 `PolicyUpdateList.getBytes()`.

   목록을 로드하려면 을 호출하십시오. `PolicyUpdateListFactory.loadPolicyUpdateList()` serialize된 목록에 전달합니다.
1. 를 호출하여 서명이 유효하고 목록이 올바른 라이선스 서버 인증서에 의해 서명되었는지 확인하십시오. `PolicyUpdateList.verifySignature()`.
1. DRM 정책 ID 전달 `String` 대상 `PolicyUpdateList.isRevoked()` 항목이 해지되었는지 확인합니다.

   또는 목록을 다음 위치에 전달할 수 있습니다. `HandlerConfiguration` 그런 다음 라이센스가 발행될 때마다 시행됩니다.
기존 항목에 더 많은 항목을 추가하려면 `PolicyUpdateList`기존 DRM 정책 업데이트 목록을 로드해야 합니다. 따라서 새 DRM을 생성해야 합니다 `PolicyUpdateListFactory` 인스턴스. 호출 `PolicyUpdateListFactory.addEntries` 이전 목록의 모든 항목을 새 목록에 추가합니다. 호출 `PolicyUpdateListFactory.addRevocationEntry` 또는 `addUpdatedEntry` DRM PolicyUpdateList에 새 해지 또는 업데이트 항목을 추가합니다.

DRM 정책 업데이트 목록을 만드는 방법을 보여 주는 샘플 코드는 다음을 참조하십시오. `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 다음에서 *참조 구현 명령줄 도구* [!DNL samples] 디렉토리.
