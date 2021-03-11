---
title: 사용자 정의 인증/자격 부여 개요(선택 사항)
description: 사용자 정의 인증/자격 부여 개요(선택 사항)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# 사용자 정의 인증/권한 개요(옵션){#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM을 구성하여 백엔드 인증/권한 부여 서비스로 연결:

* 이 사용자는 라이선스를 취득할 수 있습니까?
* 라이센스에 어떤 권리/제한이 있어야 합니까?

Primetime Cloud DRM에는 백엔드 인증/권한 부여 서비스에 대한 참조 구현이 포함되어 있습니다. 이 서버는 데모용으로 BEES 요청에 대해 &quot;허용&quot; 응답을 제공합니다. 서버 비헤이비어를 수정하려면 [!DNL BEESServlet.java]을(를) 참조하십시오.

>[!NOTE]
>
>이전에는 이 제품이 *백엔드 자격 부여 서버*(BEES)라는 별도의 제품으로 이 문서와 소스 파일에서 BEES에 대한 참조를 포함하고 있었습니다.

