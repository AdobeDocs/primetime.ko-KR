---
seo-title: DRM 정책 중요성
title: DRM 정책 중요성
uuid: ddc03142-7acb-4a9f-a367-e34cfc5e78ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# DRM 정책 중요성{#drm-policy-criticality}

DRM 정책에 새 사용 규칙을 적용할 계획이며, 이전 라이센스 서버에 대해 패키지되어 있고 새로운 사용 규칙을 올바로 해석하지 못하는 컨텐츠에 이 DRM 정책을 사용하려는 경우 이전 라이센스 서버의 작동 방식을 지정해야 할 수 있습니다. 기본적으로 DRM 정책 중요도는 로 `true`설정됩니다.

이 설정은 라이센스 서버가 지정된 DRM 정책을 사용하는 라이센스를 생성하기 전에 DRM 정책의 모든 부분을 처리해야 함을 나타냅니다. DRM 정책 중요도가 로 설정된 `false`경우 이전 라이선스 서버는 DRM 정책의 해당 부분을 무시하고 올바로 해석하지 못할 수 있습니다. 따라서 서버에서 생성된 모든 라이선스에는 새로운 사용 규칙이 포함되지 않습니다.

SDK 버전 2.0.2 이상을 지원하는 Primetime DRM 서버는 DRM 정책 중요도 설정을 수락합니다.
