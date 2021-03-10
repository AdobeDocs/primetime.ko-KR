---
description: 정책 설정은 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 시기와 방법에 대한 조건을 지정하는 프로세스입니다.
title: 정책 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 정책 설정{#setting-policies}

정책 설정은 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 시기와 방법에 대한 조건을 지정하는 프로세스입니다.

정책 만들기는 라이선스 토큰 요청의 일부로 발생합니다. (Widevine 사용 예제는 [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request)을 참조하십시오.)

고객의 서버측 코드가 권한 확인, 지리적 위치 또는 기타 필요한 정보를 기반으로 라이센스를 발급한다고 판단하면 토큰이 요청되고, 토큰&#x200B;*에서*&#x200B;이 필요한 `securityLevel`, `hdcpOutputControl` 및 `licenseDuration`를 지정합니다. 이러한 옵션은 무선 정책의 클라이언트측 옵션입니다. 다른 DRM 솔루션도 유사한 접근 방식을 제공하지만 세부 사항은 서로 다르며 개별 워크플로우에서 자세히 설명합니다.

>[!NOTE]
>
>Adobe은 자체 자격 부여 서버/스토어프런트를 구현하는 방법을 보여주는 샘플 참조 서버를 제공합니다.[참조 서버:샘플 ExpressPlay 자격 부여 서버(SEE)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

