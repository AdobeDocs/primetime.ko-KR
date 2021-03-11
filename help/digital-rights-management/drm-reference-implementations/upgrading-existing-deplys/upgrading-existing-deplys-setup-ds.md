---
title: 도메인 서버 설정
description: 도메인 서버 설정
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# 도메인 서버{#set-up-a-domain-server} 설정

기존 라이센스 서버 설치에 도메인 서버를 구성하려면:

1. [!DNL tomcat/lib] 디렉토리에서 [!DNL flashaccess-refimpl.properties] 파일을 엽니다.
1. `Domain CA certificate` 옵션에서 도메인 CA 인증서를 완료합니다.

   그런 다음 이 인증서는 도메인 토큰을 수락하는 데 사용됩니다.
1. `Domain CA credential` 옵션 아래에서 `Domain CA credential certificate (PFX)` 세부 정보를 완료합니다.

   그런 다음 이 인증서는 도메인 인증서 및 토큰 서명에 사용됩니다.
1. `DomainServerlURL`의 값을 지정합니다.

   이 값을 `NULL`으로 설정하면 도메인 인증이 성공할 수 있습니다. 그러나 도메인에 참여하는 동안 도메인 연결 오류가 발생할 수 있습니다.
