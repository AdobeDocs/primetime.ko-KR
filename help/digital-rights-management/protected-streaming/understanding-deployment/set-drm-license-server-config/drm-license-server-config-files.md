---
title: 라이센스 서버 구성 파일
description: 라이센스 서버 구성 파일
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 라이센스 서버 구성 파일{#license-server-configuration-files}

보호된 스트리밍을 위한 Adobe Primetime DRM Server에는 다음과 같은 유형의 구성 파일이 필요합니다.

* 전역 구성 파일( [!DNL flashaccess-global.xml])
* 각 테넌트에 대한 테넌트 구성 파일( [!DNL flashaccess-tenant.xml])

구성 파일 편집을 완료한 후 보호된 스트리밍을 위해 Primetime DRM Server와 함께 제공된 유틸리티를 사용하여 파일이 제대로 구성되어 있는지 확인하는 것이 좋습니다.

*구성 유효성 검사기*&#x200B;를 참조하십시오.

구성 파일의 투명한 텍스트에서 암호를 사용할 수 없도록 하려면 Adobe에서 제공한 Scrambler 도구를 사용하여 전역 및 테넌트 구성 파일에 지정한 모든 암호를 암호화해야 합니다.

암호 암호화 방법에 대한 자세한 내용은 *암호 스크램블러*&#x200B;를 참조하십시오.
