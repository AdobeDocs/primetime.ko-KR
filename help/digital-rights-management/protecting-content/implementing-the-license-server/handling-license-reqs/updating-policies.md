---
seo-title: DRM 정책 업데이트
title: DRM 정책 업데이트
uuid: 6f7a1432-88e4-499b-a008-6c8cf0e9c09b
translation-type: tm+mt
source-git-commit: d5986e9bc8689bf37abdf242a41aea5e768df754

---


# DRM 정책 업데이트 {#updating-drm-policies}

콘텐트를 패키지한 후 DRM 정책이 업데이트되는 경우 라이선스 서버에 업데이트된 DRM 정책을 제공하여 라이선스 발행 시 업데이트된 버전을 사용할 수 있습니다. 라이선스 서버에서 DRM 정책을 저장하기 위한 데이터베이스에 액세스할 수 있는 경우 데이터베이스에서 업데이트된 DRM 정책을 검색하여 새 버전의 DRM 정책을 `LicenseRequestMessage.setSelectedPolicy()` 제공하도록 호출할 수 있습니다.

중앙 데이터베이스를 사용하지 않는 라이센스 서버의 경우 SDK는 DRM 정책 업데이트 목록을 지원합니다. DRM 정책 업데이트 목록은 업데이트되거나 해지된 DRM 정책 목록을 포함하는 파일입니다. DRM 정책이 업데이트되면 새 DRM 정책 업데이트 목록을 생성하고 목록을 정기적으로 모든 라이센스 서버에 푸시합니다. 설정을 통해 목록을 SDK로 `HandlerConfiguration.setPolicyUpdateList()`전달합니다. 업데이트 목록이 제공된 경우 SDK는 컨텐츠 메타데이터를 구문 분석할 때 이 목록을 참조합니다. `ContentInfo.getUpdatedPolicies()` 메타데이터에 지정된 DRM 정책의 업데이트된 버전이 포함되어 있습니다.

DRM [정책 및 DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) 정책 [업데이트 목록 작업 참조](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)