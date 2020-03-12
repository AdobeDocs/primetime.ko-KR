---
seo-title: 사용자 정의 인증/권한 개요(선택 사항)
title: 사용자 정의 인증/권한 개요(선택 사항)
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 사용자 정의 인증/권한 개요(선택 사항){#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM은 자신의 백엔드 인증/권한 부여 서비스에 연결되도록 구성하여 다음을 결정할 수 있습니다.

* 이 사용자가 라이선스를 취득할 수 있습니까?
* 라이센스에 어떤 권리/제한이 있어야 합니까?

Primetime Cloud DRM에는 백엔드 인증/권한 부여 서비스의 참조 구현이 포함되어 있습니다. 데모용으로 이 서버는 BEES 요청에 대한 &quot;허용&quot; 응답을 발행하고 있습니다. 서버 비헤이비어를 [!DNL BEESServlet.java] 수정하려면 을 참조하십시오.

>[!NOTE]
>
>이전에는 BEES(Back End *Entitlement Server* )라는 별도의 제품으로 이 문서와 소스 파일에서 BEES에 대한 참조가 사용되었습니다.

