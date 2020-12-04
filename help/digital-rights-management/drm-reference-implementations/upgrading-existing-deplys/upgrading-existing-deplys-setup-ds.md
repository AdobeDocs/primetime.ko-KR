---
description: 'null'
seo-description: 'null'
seo-title: 도메인 서버 설정
title: 도메인 서버 설정
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 도메인 서버 설정{#set-up-a-domain-server}

기존 라이센스 서버 설치에 도메인 서버를 구성하려면:

1. [!DNL tomcat/lib] 디렉토리에서 [!DNL flashaccess-refimpl.properties] 파일을 엽니다.
1. `Domain CA certificate` 옵션에서 도메인 CA 인증서를 완료합니다.

   이 인증서는 도메인 토큰을 수락하는 데 사용됩니다.
1. `Domain CA credential` 옵션 아래에서 `Domain CA credential certificate (PFX)` 세부 정보를 완료합니다.

   이 인증서는 도메인 인증서 및 토큰을 서명하는 데 사용됩니다.
1. `DomainServerlURL`에 대한 값을 지정합니다.

   이 값이 `NULL`으로 설정된 경우 도메인 인증이 성공할 수 있습니다. 하지만 도메인에 가입하는 동안 도메인 가입 오류가 발생할 수 있습니다.
