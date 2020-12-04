---
seo-title: 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리
title: 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리 {#maintain-a-allowlist-of-trusted-content-packagers}

**허용 목록**&#x200B;은 신뢰할 수 있는 엔티티 목록입니다. 컨텐츠 패키저의 경우 컨텐츠 소유자가 FLV/F4V 비디오 파일을 패키징(또는 암호화)하여 DRM으로 보호된 컨텐츠를 만드는 것으로 신뢰하는 조직입니다. Adobe 액세스 권한을 배포할 때는 신뢰할 수 있는 콘텐츠 패키저의 허용 목록을 유지하고 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터(DRM 헤더)에 포함된 콘텐츠 패키저 ID를 확인하는 것이 좋습니다.

콘텐츠를 패키지한 엔터티에 대한 정보를 얻는 방법에 대한 자세한 내용은 *Adobe 액세스 API 참조*&#x200B;의 `V2ContentMetaData.getPackagerInfo()`을 참조하십시오.
