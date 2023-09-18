---
title: BEES 개요
description: BEES 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# BEES 개요{#bees-overview}

BEES(백엔드 권한 부여 서비스)를 구현하여 Primetime Cloud DRM 작업에 대한 사용자 정의 권한을 제공할 수 있습니다.

Primetime Cloud DRM은 기본적으로 익명 라이선스 전달을 사용합니다. 즉, Primetime Cloud DRM으로 전송된 모든 라이선스 요청은 추가적인 인증/권한 부여 검사를 수행하지 않고 유효한 라이선스를 반환합니다(Adobe Primetime 인증 사용을 호출하는 정책 제약 조건을 적용하지 않은 경우).

라이센스 요청에는 컨텐츠의 패키징/암호화 중에 사용된 DRM 정책이 포함되어 있습니다. DRM 정책은 클라이언트에 반환되는 DRM 라이센스를 생성하는 데 사용됩니다. 기본 시나리오에서는 컨텐츠 패키징 시간에 모든 DRM 정책을 결정해야 합니다. 이러한 워크플로를 보다 세밀하게 제어하려는 고객은 다음 옵션을 사용할 수 있습니다.

1. Primetime 인증을 통합하여 재생 전에 추가 권한 검사를 추가합니다.
1. 패키징된 콘텐츠를 모든 장치가 재생할 수 있도록 하기 전에 Primetime Cloud DRM이 쿼리하는 온-프레미스 권한 서비스를 만듭니다.

온프레미스 권한 부여 서비스는 다음 두 가지 데이터를 포함하는 Primetime Cloud DRM에 응답을 제공해야 합니다.

* `isAllowed`
* `drmPolicyToUse`

이러한 설정은 장치가 컨텐츠를 재생할 수 있는지 여부와 DRM 라이센스(인 경우)를 생성하는 데 사용할 DRM 정책을 결정합니다 `isAllowed` 은 true)입니다.

이 문서에서는 위의 옵션 2를 수행하기 위해 수행해야 하는 작업을 다룹니다. 고유한 온프레미스 외부 권한 부여 서비스를 구현하고 패키징한 콘텐츠에 대해 Primetime Cloud DRM에서 사용할 수 있도록 설정.
