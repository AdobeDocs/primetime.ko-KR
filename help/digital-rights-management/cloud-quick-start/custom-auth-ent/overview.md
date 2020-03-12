---
seo-title: BEES 파섹
title: BEES 파섹
uuid: c6ee7528-fdfa-4a56-bea2-a5e2dab6d428
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# BEES 파섹{#bees-overview}

백엔드 권한 부여 서비스(BEES)를 구현하여 Primetime Cloud DRM 작업에 대한 사용자 정의 자격 부여를 제공할 수 있습니다.

Primetime Cloud DRM은 기본적으로 익명 라이선스 제공을 사용합니다. 즉, Primetime Cloud DRM으로 전송된 모든 라이선스 요청은 추가 인증/인증 검사를 수행하지 않고 유효한 라이선스를 반환하게 됩니다(Adobe Primetime 인증 사용을 요청하는 정책 제약 조건을 적용하지 않은 경우).

라이센스 요청에는 컨텐츠의 패키징/암호화 중에 사용된 DRM 정책이 포함되어 있습니다. DRM 정책은 클라이언트에 반환된 DRM 라이센스를 생성하는 데 사용됩니다. 기본 시나리오에서는 컨텐츠 패키징 시 모든 DRM 정책 결정을 내려야 합니다. 이러한 워크플로우를 보다 세밀하게 제어하려는 고객은 다음 옵션을 사용할 수 있습니다.

1. Primetime 인증을 통합하여 재생 전에 권한 부여 검사를 추가로 추가할 수 있습니다.
1. Primetime Cloud DRM이 쿼리하는 온-프레미스 권한 부여 서비스를 만들어 모든 장치에서 패키지된 콘텐츠를 재생할 수 있도록 허용합니다.

온-프레미스 권한 부여 서비스는 다음 두 가지 데이터가 포함된 Primetime Cloud DRM에 대한 응답을 제공해야 합니다.

* `isAllowed`
* `drmPolicyToUse`

이렇게 하면 장치가 내용을 재생할 수 있는지 여부와 DRM 라이센스를 생성하는 데 사용할 DRM 정책( `isAllowed` true인 경우)이 결정됩니다.

이 문서에서는 위의 옵션 2를 수행하기 위해 필요한 작업에 대해 설명합니다.사내 외부 권한 부여 서비스를 구현하고 Primetime Cloud DRM에서 패키징한 콘텐츠를 이용할 수 있습니다.
