---
title: DRM 정책 중요성
description: DRM 정책 중요성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# DRM 정책 중요성{#drm-policy-criticality}

DRM 정책에 새 사용 규칙을 적용할 계획이며, 이전 라이센스 서버에 대해 패키지화된 컨텐츠에서 이 DRM 정책을 사용할 계획인 경우(따라서 새 사용 규칙을 제대로 해석하지 않음) 이전 라이센스 서버의 작동 방식을 지정해야 할 수 있습니다. 기본적으로 DRM 정책 중요도는 `true`으로 설정됩니다.

이 설정은 지정된 DRM 정책을 사용하는 라이선스를 생성하려면 라이센스 서버가 DRM 정책의 모든 부분을 처리해야 함을 나타냅니다. DRM 정책 중요도가 `false`으로 설정된 경우 이전 라이선스 서버는 DRM 정책의 해당 부분을 올바로 해석할 수 없습니다. 따라서 서버에서 생성된 모든 라이선스에는 새로운 사용 규칙이 포함되지 않습니다.

SDK 버전 2.0.2 이상을 지원하는 Primetime DRM 서버가 DRM 정책 중요 설정을 수락합니다.
