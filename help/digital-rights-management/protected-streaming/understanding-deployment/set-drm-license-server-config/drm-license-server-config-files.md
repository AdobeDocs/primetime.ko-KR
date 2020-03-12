---
seo-title: 라이센스 서버 구성 파일
title: 라이센스 서버 구성 파일
uuid: 7c7e0f76-2ced-45af-9542-99e06ec31cda
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이센스 서버 구성 파일{#license-server-configuration-files}

보호된 스트리밍을 위한 Adobe Primetime DRM Server에는 다음과 같은 유형의 구성 파일이 필요합니다.

* 전역 구성 파일( [!DNL flashaccess-global.xml])
* 각 테넌트( [!DNL flashaccess-tenant.xml])에 대한 테넌트 구성 파일

구성 파일 편집을 완료한 후 보호된 스트리밍을 위해 Primetime DRM Server와 함께 제공된 유틸리티를 사용하여 파일의 형식이 올바른지 확인하는 것이 좋습니다.

구성 *유효성 검사기를 참조하십시오*.

구성 파일의 투명한 텍스트로 암호를 사용하지 않으려면 Adobe에서 제공한 Scrambler 도구를 사용하여 전역 및 테넌트 구성 파일에서 지정한 모든 암호를 암호화해야 합니다.

암호 *암호화에* 대한 자세한 내용은 암호 스크램블러를 참조하십시오.
