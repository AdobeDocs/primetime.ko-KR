---
title: 인증서 갱신
description: 인증서 갱신
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# 인증서 갱신{#renew-certificates}

Adobe Primetime DRM SDK 구성을 기반으로 하는 다음과 같은 인증서 갱신 제한 사항을 알고 있어야 합니다.

* Primetime DRM Production SDK

   Adobe은 지원 계약을 구입할 때 Primetime DRM Production SDK에 대한 무료 인증서의 초기 세트를 제공합니다. 지원 계약이 없는 경우 2년 동안 유효한 갱신 인증서 세트를 구입할 수 있습니다.
* Primetime DRM 평가 SDK

   이 SDK에 대해 설정된 인증서는 1년 동안 유효하며 갱신할 수 없습니다.
* Primetime DRM 시험버전 SDK

   Primetime DRM 시험판 SDK는 3개월 동안 유효하며 Adobe은 한 세트의 무료 갱신 인증서를 제공합니다.

## 새 인증서 구현 및 기존 컨텐츠 {#section_345C92D1C9794B0BBB9A9B0702EC95FF}에 대한 이전 인증서 사용

Primetime DRM에서 라이선스 서버가 이전(또는 만료된) 패키지 인증서로 패키지화된 콘텐츠에 대한 라이선스를 발급하도록 허용할 수 있습니다. 이전에 패키지한 내용에서 라이센스 요청을 수락하도록 서버를 구성하려면 서버에 이전 인증서를 제공하고 서버에서 이전 인증서를 찾을 위치를 알 수 있도록 서버의 구성 파일을 업데이트하십시오. 자세한 내용은 *콘텐트 보호를 위해 Adobe Primetime DRM SDK 사용*&#x200B;에서 Adobe에서 발행한 인증서가 만료될 때 인증서 업데이트 처리를 참조하십시오.**

서버 애플리케이션이 Primetime DRM 참조 구현 기술을 기반으로 하는 경우 서버측 프로그램을 업데이트할 필요가 없습니다. `flashaccess-refimpl.properties` 파일에는 추가 전송 및 라이센스 서버 인증서를 지정할 수 있는 필드가 있습니다. 하나의 인증서만 있으면 해당 속성을 채울 필요가 없습니다. 인증서가 만료되고 라이센스 응답을 발행할 때 이러한 인증서를 사용하려면 구성 파일에 이러한 인증서를 제공하고 서버를 다시 시작해야 합니다.

이전 인증서를 지정하려면 다음 속성을 사용합니다.

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

