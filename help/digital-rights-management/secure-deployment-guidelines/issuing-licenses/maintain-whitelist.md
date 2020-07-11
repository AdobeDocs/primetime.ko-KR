---
description: 허용 목록은 신뢰할 수 있는 엔티티 목록입니다.
seo-description: 허용 목록은 신뢰할 수 있는 엔티티 목록입니다.
seo-title: 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리
title: 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리 {#maintain-a-allowlist-of-trusted-content-packagers}

허용 목록은 신뢰할 수 있는 엔티티 목록입니다.

컨텐츠 패키저의 경우, 개체는 컨텐츠 소유자가 비디오 파일을 패키지화(또는 암호화)하고 DRM으로 보호된 컨텐츠를 만드는 것으로 신뢰하는 조직입니다. Adobe Primetime DRM을 배포할 때는 신뢰할 수 있는 콘텐츠 패키저의 허용 목록을 유지 관리해야 합니다. 또한 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터에서 컨텐츠 패키저 ID를 확인해야 합니다.

컨텐츠를 패키지한 엔터티에 대한 정보를 얻는 방법을 알아보려면 [V2ContentMetaData.getPackagerInfo()를 참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
