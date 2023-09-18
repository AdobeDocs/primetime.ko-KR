---
title: DRM 정책 중요도
description: DRM 정책 중요도
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# DRM 정책 중요도{#drm-policy-criticality}

DRM 정책에 새 사용 규칙을 적용하고 이전 라이선스 서버에 대해 패키지화된(따라서 새 사용 규칙을 올바르게 해석하지 않음) 콘텐츠에서 이 DRM 정책을 사용하려는 경우 이전 라이선스 서버의 동작 방식을 지정해야 할 수 있습니다. 기본적으로 DRM 정책 중요도는 `true`.

이 설정은 지정된 DRM 정책을 사용하는 라이선스를 생성하기 전에 라이선스 서버가 DRM 정책의 모든 부분을 처리해야 함을 나타냅니다. DRM 정책 중요도가 `false`로 설정하면 이전 라이센스 서버에서 올바르게 해석할 수 없는 DRM 정책 부분을 무시할 수 있습니다. 따라서 서버에서 생성된 라이센스에는 새 사용 규칙이 포함되지 않습니다.

SDK 버전 2.0.2 이상을 지원하는 Primetime DRM 서버는 DRM 정책 중요도 설정을 수락합니다.
