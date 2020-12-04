---
description: 고객은 외부 CEK 기능과 함께 자체 CKMS(Content Key Management Systems)와 함께 AAXS(Adobe 액세스) DRM을 사용할 수 있습니다.
seo-description: 고객은 외부 CEK 기능과 함께 자체 CKMS(Content Key Management Systems)와 함께 AAXS(Adobe 액세스) DRM을 사용할 수 있습니다.
seo-title: Adobe 액세스 DRM 외부 CEK 개요
title: Adobe 액세스 DRM 외부 CEK 개요
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Adobe 액세스 DRM 외부 CEK 개요 {#adobe-access-drm-external-cek-overview}

고객은 외부 CEK 기능과 함께 자체 CKMS(Content Key Management Systems)와 함께 AAXS(Adobe 액세스) DRM을 사용할 수 있습니다.

기본적으로 AAXS(Adobe 액세스) DRM은 컨텐츠 패키징 프로세스 동안 키, 인증서 및 DRM 메타데이터를 직접 처리해야 하는 필요성을 추상화합니다. AAXS Java SDK는 패키징 시간 동안 CEK(Random Content Encryption Key)를 자동으로 생성하고 이를 사용하여 컨텐츠를 암호화합니다. 그 다음 SDK는 CEK 자체를 암호화하여 컨텐츠의 메타데이터에 삽입합니다. 라이선스 발급 시 AAXS 서버는 라이선스를 생성하기 위해 메타데이터에서 CEK에 액세스하려면 AAXS 라이센스 서버 개인 키만 필요합니다.
