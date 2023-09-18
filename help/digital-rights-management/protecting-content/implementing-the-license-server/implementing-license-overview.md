---
title: 라이선스 서버 개요
description: 라이선스 서버 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 개요 {#license-server-overview}

클라이언트에 라이선스를 발급하려면 먼저 Adobe Primetime DRM 라이선스 서버를 배포해야 합니다. 라이센스 서버는 Primetime DRM SDK를 사용하여 다양한 작업을 수행합니다.

라이센스 서버를 구현하려면

* 사용자 이름/암호 인증이 지원되는 경우 인증 요청을 처리합니다.
* 라이선스 요청 처리
* 서버 버전 가져오기 요청 처리 - 모든 서버는 이 유형의 요청에 대한 지원을 구현해야 합니다.
* 도메인 등록 요청 처리 - 도메인 서버를 구현하는 경우에만 필요합니다.
* 도메인 등록 취소 요청 처리 - 도메인 서버를 구현하는 경우에만 필요합니다.
* 프로세스 동기화 - 라이센스가 동기화 요구 사항을 지정하는 경우에만 필요합니다.

또한 서버는 사용자를 인증하고, 사용자가 콘텐츠를 볼 수 있는 권한이 있는지 확인하고, 선택적으로 라이선스 사용을 추적할 수 있는 비즈니스 논리를 제공해야 합니다.

다음을 참조하십시오 *Adobe Primetime DRM API 참조* Java API에 대한 자세한 내용.
