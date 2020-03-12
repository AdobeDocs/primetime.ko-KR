---
description: 정책 설정은 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 시기와 방법에 대한 조건을 지정하는 프로세스입니다.
seo-description: 정책 설정은 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 시기와 방법에 대한 조건을 지정하는 프로세스입니다.
seo-title: 정책 설정
title: 정책 설정
uuid: 2d2672ce-5ed4-4868-aa5e-0a9e21a809b3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 정책 설정{#setting-policies}

정책 설정은 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 시기와 방법에 대한 조건을 지정하는 프로세스입니다.

정책 만들기는 라이센스 토큰 요청의 일부로 발생합니다. (Widevine [사용](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) 예는 https://www.expressplay.com/developer/restapi/#widevine-license-token-request을 참조하십시오.)

고객의 서버측 코드가 권한 확인, 지리적 위치 또는 기타 필요한 정보를 기반으로 라이센스를 발급하기로 결정되면, 토큰을 요청하고 토큰에 *필요한* 및 `securityLevel``hdcpOutputControl``licenseDuration`를 지정합니다. 이는 무선 정책에 대한 클라이언트측 옵션입니다. 다른 DRM 솔루션도 유사한 접근 방식을 제공하지만 세부 사항은 각 사례마다 다르며 개별 워크플로우에서 자세히 설명합니다.

>[!NOTE]
>
>Adobe는 자체 권한 부여 서버/스토어프런트 구현을 보여주는 샘플 참조 서버를 제공합니다.참조 [서버:샘플 ExpressPlay 권한 부여 서버(SEE)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

