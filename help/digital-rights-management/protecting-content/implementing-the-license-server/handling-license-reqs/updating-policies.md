---
title: DRM 정책 업데이트
description: DRM 정책 업데이트
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# DRM 정책 업데이트 {#updating-drm-policies}

콘텐츠가 패키징된 후 DRM 정책이 업데이트되면 라이센스 서버에 업데이트된 DRM 정책을 제공하여 라이센스를 발급할 때 업데이트된 버전을 사용할 수 있도록 합니다. 라이센스 서버에서 DRM 정책을 저장하기 위한 데이터베이스에 액세스할 수 있는 경우 데이터베이스에서 업데이트된 DRM 정책을 검색하고 를 호출할 수 있습니다 `LicenseRequestMessage.setSelectedPolicy()` DRM 정책의 새 버전을 제공합니다.

중앙 데이터베이스에 의존하지 않는 라이선스 서버의 경우, SDK는 DRM 정책 업데이트 목록을 지원합니다. DRM 정책 업데이트 목록은 업데이트되거나 취소된 DRM 정책 목록을 포함하는 파일입니다. DRM 정책이 업데이트되면 새 DRM 정책 업데이트 목록 을 생성하고 이 목록을 모든 라이센스 서버에 정기적으로 푸시합니다. 를 설정하여 목록을 SDK에 전달 `HandlerConfiguration.setPolicyUpdateList()`. 업데이트 목록이 제공된 경우 SDK는 콘텐츠 메타데이터를 구문 분석할 때 이 목록을 참조합니다. `ContentInfo.getUpdatedPolicies()` 는 메타데이터에 지정된 DRM 정책의 업데이트된 버전을 포함합니다.

다음을 참조하십시오 [DRM 정책 작업](../../../protecting-content/working-policies-overview/working-with-policies.md) 및 [DRM 정책 업데이트 목록](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
