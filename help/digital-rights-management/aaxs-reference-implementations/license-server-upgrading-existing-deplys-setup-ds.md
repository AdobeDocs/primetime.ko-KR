---
title: 도메인 서버 설정
description: 도메인 서버 설정
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 도메인 서버 {#set-up-a-domain-server} 설정

기존 라이센스 서버 설치에서 도메인 서버를 구성하려면 다음 작업을 수행하십시오.

1. [!DNL tomcat/lib] 아래에서 [!DNL flashaccess-refimpl.properties] 파일을 엽니다.

1. `Domain CA certificate` 옵션에서 도메인 CA 인증서 세부 사항을 채웁니다. 이 인증서는 도메인 토큰을 수락하는 데 사용됩니다.
1. `Domain CA credential` 옵션에서 `Domain CA credential certificate (PFX)` 세부 정보를 입력합니다. 이 인증서는 도메인 인증서 및 토큰 서명에 사용됩니다.

1. `DomainServerlURL`의 값을 지정합니다. 이 값이 NULL이면 도메인 인증이 성공할 수 있습니다. 그러나 도메인에 가입하는 동안 도메인 연결 오류가 발생합니다.

