---
description: Adobe Primetime DRM을 사용하여 Adobe에 의해 게시된 시스템 CRL을 보완하는 CRL을 생성할 수 있습니다.
seo-description: Adobe Primetime DRM을 사용하여 Adobe에 의해 게시된 시스템 CRL을 보완하는 CRL을 생성할 수 있습니다.
seo-title: Adobe에서 게시한 CRL을 보완하기 위해 CRL 생성
title: Adobe에서 게시한 CRL을 보완하기 위해 CRL 생성
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# Adobe{#generating-crls-to-supplement-those-published-by-adobe}에서 게시한 CRL을 보완하기 위해 CRL 생성

Adobe Primetime DRM을 사용하여 Adobe에 의해 게시된 시스템 CRL을 보완하는 CRL을 생성할 수 있습니다.

Primetime DRM SDK는 Adobe CRL을 확인하고 적용합니다. 그러나 CRL을 Primetime DRM SDK에 전달하여 추가 시스템 자격 증명을 호출하는 CRL을 만들어 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 라이센스를 발급할 때 SDK는 Adobe CRL과 CRL을 확인합니다.

CRL을 생성하려면 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)를 참조하십시오.
