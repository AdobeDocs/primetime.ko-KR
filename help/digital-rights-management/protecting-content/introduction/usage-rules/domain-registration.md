---
title: 장치 그룹 도메인 등록
description: 장치 그룹 도메인 등록
copied-description: true
exl-id: 81d6023b-76e0-4786-805b-bfe77e9f8513
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# 장치 그룹 도메인 등록{#device-group-domain-registration}

특정 디바이스에 라이센스를 바인딩하는 대신 Primetime DRM 3.0 이상에서는 디바이스 도메인에 라이센스를 바인딩할 수 있습니다.

여러 장치가 도메인에 가입하고 도메인 토큰을 받을 수 있습니다. 도메인의 장치가 라이선스를 획득한 후 라이선스를 도메인의 다른 장치로 전송할 수 있으며, 해당 장치는 라이선스 서버로부터 직접 라이선스를 획득하지 않고 콘텐츠를 재생할 수 있습니다.

도메인 바인딩 라이선스를 지원하려면 Primetime DRM 정책은 클라이언트가 등록해야 하는 도메인 서버를 지정해야 합니다. Primetime DRM 정책은 익명 액세스를 사용할지 또는 서버에 사용자 이름/암호 또는 사용자 지정 인증이 필요한지 여부에 관계없이 도메인 서버에 대한 인증 요구 사항도 지정해야 합니다.

도메인 등록 및 도메인 바인딩 라이선스는 Primetime DRM 클라이언트 버전 3.0 이상에서 지원됩니다. 이전 클라이언트 또는 Flash Player의 Adobe Primetime 3.0 클라이언트가 도메인 등록을 지원하는 콘텐츠에 대한 라이선스를 요청하는 경우 라이선스 서버는 대체 Primetime DRM 정책을 사용하여 특정 장치에 대한 바인딩을 지원하는 라이선스를 발급할 수 있습니다.
