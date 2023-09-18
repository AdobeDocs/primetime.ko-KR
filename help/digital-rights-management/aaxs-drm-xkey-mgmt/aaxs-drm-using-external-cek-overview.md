---
description: 고객은 외부 CEK 기능이 있는 자체 CKMS(Content Key Management Systems)와 함께 AAXS(Adobe 액세스) DRM을 사용할 수 있습니다.
title: Adobe 액세스 DRM 외부 CEK 개요
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Adobe 액세스 DRM 외부 CEK 개요 {#adobe-access-drm-external-cek-overview}

고객은 외부 CEK 기능이 있는 자체 CKMS(Content Key Management Systems)와 함께 AAXS(Adobe 액세스) DRM을 사용할 수 있습니다.

AAXS(Adobe 액세스) DRM은 기본적으로 콘텐츠 패키징 프로세스 중에 키, 인증서 및 DRM 메타데이터를 직접 처리해야 하는 필요성을 추상화합니다. AAXS Java SDK는 패키징 시간 동안 무작위 CEK(콘텐츠 암호화 키)를 자동으로 생성하고, 이를 사용하여 콘텐츠를 암호화합니다. 그런 다음 SDK는 CEK 자체를 암호화하고 콘텐츠의 메타데이터에 삽입합니다. 라이센스 발행 시 AAXS 서버는 메타데이터를 통해 CEK에 액세스하여 라이센스를 생성하기 위한 AAXS 라이센스 서버 개인 키만 있으면 됩니다.
