---
description: Adobe Primetime DRM을 사용하여 Adobe에 의해 게시된 시스템 CRL을 보완하는 CRL을 생성할 수 있습니다.
title: Adobe에 의해 게시된 항목을 보완하기 위해 CRL 생성
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Adobe에 의해 게시된 항목을 보완하기 위해 CRL 생성{#generating-crls-to-supplement-those-published-by-adobe}

Adobe Primetime DRM을 사용하여 Adobe에 의해 게시된 시스템 CRL을 보완하는 CRL을 생성할 수 있습니다.

Primetime DRM SDK는 Adobe CRL을 확인하고 시행합니다. 그러나 CRL을 Primetime DRM SDK에 전달하여 추가 컴퓨터 자격 증명을 취소하는 CRL을 생성하여 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 라이센스를 발급하면 SDK가 Adobe CRL과 CRL을 확인합니다.

CRL을 생성하려면 다음을 참조하십시오 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
