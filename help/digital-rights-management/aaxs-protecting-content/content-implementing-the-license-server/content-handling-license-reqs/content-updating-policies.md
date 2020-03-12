---
seo-title: 정책 업데이트
title: 정책 업데이트
uuid: f6686c8b-bedf-4ec5-a14e-f03326519f89
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 정책 업데이트 {#updating-policies}

컨텐츠가 패키지된 후 정책이 업데이트되는 경우 라이선스 서버에 업데이트된 정책을 제공하여 라이선스 발행 시 업데이트된 버전을 사용할 수 있도록 합니다. 라이센스 서버에서 정책을 저장할 데이터베이스에 대한 액세스 권한을 가지고 있는 경우 데이터베이스에서 업데이트된 정책을 검색하고 새 버전의 정책을 `LicenseRequestMessage.setSelectedPolicy()` 제공하도록 호출할 수 있습니다.

중앙 데이터베이스를 사용하지 않는 라이센스 서버의 경우 SDK는 정책 업데이트 목록에 대한 지원을 제공합니다. 정책 업데이트 목록은 업데이트되거나 취소된 정책 목록이 포함된 파일입니다. 정책이 업데이트되면 새 정책 업데이트 목록을 생성하고 목록을 정기적으로 모든 라이센스 서버에 푸시합니다. 설정을 통해 목록을 SDK로 `HandlerConfiguration.setPolicyUpdateList()`전달합니다. 업데이트 목록이 제공된 경우 SDK는 컨텐츠 메타데이터를 구문 분석할 때 이 목록을 참조합니다. `ContentInfo.getUpdatedPolicies()` 에 메타데이터에 지정된 정책의 업데이트된 버전이 포함되어 있습니다.

정책 [및 정책 업데이트](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) 목록을 [사용한 작업을 참조하십시오.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
