---
description: 허용 목록은 신뢰할 수 있는 엔티티 목록입니다.
title: 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리 {#maintain-a-allowlist-of-trusted-content-packagers}

허용 목록은 신뢰할 수 있는 엔티티 목록입니다.

콘텐츠 패키지의 경우 콘텐츠는 콘텐츠 소유자가 비디오 파일을 패키지화(또는 암호화)하고 DRM 보호 컨텐츠를 만들 수 있다고 신뢰하는 조직입니다. Adobe Primetime DRM을 배포할 때 신뢰할 수 있는 컨텐츠 패키저의 허용 목록을 유지 관리해야 합니다. 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터에서 콘텐츠 패키저 ID를 확인해야 합니다.

내용을 패키지화한 엔터티에 대한 정보를 얻는 방법에 대해 알아보려면 [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())를 참조하십시오.
