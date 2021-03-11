---
title: 도메인 바인딩된 라이선스 발급
description: 도메인 바인딩된 라이선스 발급
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# 도메인 바인딩된 라이선스 발급 {#issuing-domain-bound-licenses}

도메인 등록이 필요한 DRM 정책을 사용하여 라이선스를 발급하려면 클라이언트의 요청에 정책에 지정된 도메인 서버에서 발행한 유효한 도메인 토큰이 포함되어야 합니다. 클라이언트가 라이센스를 요청하면 도메인 서버에 등록한 컨텐츠 메타데이터에 지정된 모든 도메인 서버에 대한 도메인 토큰이 자동으로 포함됩니다. 선택한 DRM 정책에 도메인 등록이 필요한 경우 SDK는 요청에서 도메인 토큰을 자동으로 선택하여 라이센스를 바인딩하거나 해당 도메인 토큰이 없는 경우 오류를 반환합니다.

도메인 토큰은 만료되지 않고 인증된 도메인 CA에서 발행된 경우 유효한 것으로 간주됩니다. 라이센스 서버는 `HandlerConfiguration.setDomainCAs()`을(를) 구성하여 도메인 토큰을 수락하는 도메인 기관을 지정해야 합니다. 도메인 CA가 구성되지 않은 경우 라이선스 서버에서 도메인 바인딩된 라이선스를 발행할 수 없습니다.

메타데이터에 여러 DRM 정책이 포함되어 있는 경우 라이선스 서버 비즈니스 로직은 클라이언트가 도메인 토큰을 제시했는지 여부를 기반으로 하는 DRM 정책을 선택할 수 있습니다. `LicenseRequestMessage.getDomainTokens()`을 사용하여 클라이언트가 등록한 도메인을 결정할 수 있습니다.
