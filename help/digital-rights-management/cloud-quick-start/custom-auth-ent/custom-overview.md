---
title: 사용자 지정 인증/권한 부여 개요(선택 사항)
description: 사용자 지정 인증/권한 부여 개요(선택 사항)
copied-description: true
exl-id: d92c4246-c772-44da-80b6-4086dfc30ff4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 사용자 지정 인증/권한 부여 개요(선택 사항){#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM은 다음을 결정하기 위해 자체 백엔드 인증/권한 부여 서비스에 연결하도록 구성할 수 있습니다.

* 이 사용자는 라이선스를 취득할 수 있습니까?
* 라이센스에 어떤 권한/제한이 적용되어야 합니까?

Primetime Cloud DRM에는 백엔드 인증/권한 부여 서비스의 참조 구현이 포함되어 있습니다. 데모 목적으로 이 서버는 BEES 요청에 &quot;허용&quot; 응답을 발행합니다. 다음을 참조하십시오 [!DNL BEESServlet.java] 서버 비헤이비어를 수정합니다.

>[!NOTE]
>
>이전에는 이라는 별도의 제품이 있었습니다. *백엔드 권한 부여 서버* (BEES). 따라서 이 문서 전체에서 그리고 소스 파일에서 BEES에 대한 참조입니다.
