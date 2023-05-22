---
title: 신뢰할 수 있는 컨텐츠 패키지 허용 목록 유지
description: 신뢰할 수 있는 컨텐츠 패키지 허용 목록 유지
copied-description: true
exl-id: 4c296d23-75c1-4d0b-a636-31b49e99c753
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 신뢰할 수 있는 컨텐츠 패키지 허용 목록 유지 {#maintain-a-allowlist-of-trusted-content-packagers}

An **허용 목록** 는 신뢰할 수 있는 엔티티 목록입니다. 콘텐츠 패키지자의 경우 FLV/F4V 비디오 파일을 패키지(또는 암호화)하기 위해 콘텐츠 소유자가 신뢰하는 조직으로, DRM 보호 콘텐츠를 만듭니다. Adobe 액세스를 배포할 때는 신뢰할 수 있는 컨텐츠 패커에 대한 허용 목록을 유지하고, 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터(DRM 헤더)에 포함된 컨텐츠 패커의 ID를 확인하는 것이 좋습니다.

콘텐츠를 패키지한 엔티티에 대한 정보를 얻는 방법에 대한 자세한 내용은 다음을 참조하십시오. `V2ContentMetaData.getPackagerInfo()` 다음에서 *Adobe 액세스 API 참조*.
