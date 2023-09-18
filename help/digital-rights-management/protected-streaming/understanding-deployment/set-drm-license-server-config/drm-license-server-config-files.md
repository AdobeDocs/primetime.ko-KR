---
title: 라이선스 서버 구성 파일
description: 라이선스 서버 구성 파일
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 라이선스 서버 구성 파일{#license-server-configuration-files}

보호된 스트리밍을 위한 Adobe Primetime DRM 서버에는 다음 유형의 구성 파일이 필요합니다.

* 전역 구성 파일( [!DNL flashaccess-global.xml])
* 각 테넌트에 대한 테넌트 구성 파일( [!DNL flashaccess-tenant.xml])

Adobe 구성 파일 편집을 완료한 후에는 Primetime DRM Server for Protected Streaming과 함께 제공되는 유틸리티를 사용하여 파일이 잘 구성되어 있는지 확인하는 것이 좋습니다.

다음을 참조하십시오 *구성 검사기*.

구성 파일에서 암호를 일반 텍스트로 사용하지 않으려면 Adobe이 제공한 Scrambler 도구를 사용하여 전역 및 테넌트 구성 파일에 지정한 모든 암호를 암호화해야 합니다.

다음을 참조하십시오 *암호 스크램블러* 암호 암호화 방법에 대한 자세한 정보.
