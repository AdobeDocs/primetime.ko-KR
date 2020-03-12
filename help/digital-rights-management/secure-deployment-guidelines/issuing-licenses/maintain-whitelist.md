---
description: 화이트 리스트는 신뢰할 수 있는 엔티티 목록입니다.
seo-description: 화이트 리스트는 신뢰할 수 있는 엔티티 목록입니다.
seo-title: 신뢰할 수 있는 컨텐츠 패키저 화이트 리스트 유지
title: 신뢰할 수 있는 컨텐츠 패키저 화이트 리스트 유지
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 신뢰할 수 있는 컨텐츠 패키저 화이트 리스트 유지{#maintain-a-whitelist-of-trusted-content-packagers}

화이트 리스트는 신뢰할 수 있는 엔티티 목록입니다.

컨텐츠 패키저의 경우, 엔티티는 컨텐츠 소유자가 비디오 파일을 패키지화(또는 암호화)하고 DRM 보호 컨텐츠를 생성하도록 신뢰하는 조직입니다. Adobe Primetime DRM을 배포할 때 신뢰할 수 있는 콘텐츠 패키저의 화이트 리스트를 유지 관리해야 합니다. 또한 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터에서 컨텐츠 패키저의 ID를 확인해야 합니다.

컨텐츠를 패키지한 엔티티에 대한 정보를 얻는 방법에 대한 자세한 내용은 V2ContentMetaData.getPackagerInfo() [를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())참조하십시오.
