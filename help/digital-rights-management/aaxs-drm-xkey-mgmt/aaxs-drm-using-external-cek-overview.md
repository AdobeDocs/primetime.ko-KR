---
description: 고객은 외부 CEK 기능과 함께 자체 CKMS(Content Key Management System)와 함께 AAXS(Adobe Access) DRM을 사용할 수 있습니다.
title: Adobe 액세스 DRM 외부 CEK 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Adobe 액세스 DRM 외부 CEK 개요 {#adobe-access-drm-external-cek-overview}

고객은 외부 CEK 기능과 함께 자체 CKMS(Content Key Management System)와 함께 AAXS(Adobe Access) DRM을 사용할 수 있습니다.

기본적으로 AAXS(Adobe Access) DRM은 컨텐츠 패키징 과정 중에 키, 인증서 및 DRM 메타데이터를 직접 처리해야 하는 필요성을 추상화합니다. AAXS Java SDK는 패키징 시간 동안 CEK(Random Content Encryption Key)를 자동으로 생성하여 컨텐츠를 암호화합니다. 그 다음에 SDK는 CEK 자체를 암호화하여 컨텐츠의 메타데이터에 삽입합니다. 라이센스 발급 시 AAXS 서버는 메타데이터를 통해 라이선스를 생성하기 위해 CEK에 액세스하려면 AAXS 라이센스 서버 전용 키만 필요합니다.
