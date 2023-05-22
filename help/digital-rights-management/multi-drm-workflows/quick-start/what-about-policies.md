---
description: 정책 설정은 사용자가 보호된 비디오 콘텐츠를 재생할 수 있는 시기와 방법에 대한 조건을 지정하는 프로세스입니다.
title: 정책 설정
exl-id: ab7295c8-88f2-4d4a-a7f1-3332df7bb735
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 정책 설정{#setting-policies}

정책 설정은 사용자가 보호된 비디오 콘텐츠를 재생할 수 있는 시기와 방법에 대한 조건을 지정하는 프로세스입니다.

정책 생성은 라이선스 토큰 요청의 일부로 수행됩니다. (참조: [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) 예를 들어, Widevine)을 사용합니다.

고객의 서버측 코드가 라이선스(자격 확인, 지리적 위치 또는 기타 필수 정보에 따름)를 발급한다고 결정하면 토큰을 요청하고 *토큰으로* 필요한 을 지정합니다. `securityLevel`, `hdcpOutputControl`, 및 `licenseDuration`. 이는 Widevine 정책에 대한 클라이언트측 옵션입니다. 다른 DRM 솔루션은 유사한 접근 방식을 제공하지만 세부 사항은 각 사례에서 다르며 개별 워크플로우에서 자세히 설명합니다.

>[!NOTE]
>
>Adobe은 고유한 자격 서버/storefront를 구현하는 방법을 보여 주는 샘플 참조 서버를 제공합니다. [참조 서버: 샘플 ExpressPlay 권한 서버(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
