---
description: Adobe Primetime DRM 파섹
seo-description: Adobe Primetime DRM 파섹
seo-title: Adobe에서 게시한 CRL을 보완하기 위한 CRL 생성
title: Adobe에서 게시한 CRL을 보완하기 위한 CRL 생성
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Adobe에서 게시한 CRL을 보완하기 위한 CRL 생성{#generating-crls-to-supplement-those-published-by-adobe}

Adobe Primetime DRM 파섹

Primetime DRM SDK는 Adobe CRL을 확인하고 적용합니다. 그러나 Primetime DRM SDK에 CRL을 전달하여 추가 시스템 자격 증명을 취소하는 CRL을 만들어 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 라이센스를 발행할 때 SDK는 Adobe CRL과 CRL을 확인합니다.

CRL을 생성하려면 RevocationListFactory를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
