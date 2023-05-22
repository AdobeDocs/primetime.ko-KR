---
title: 도메인 서버 설정
description: 도메인 서버 설정
copied-description: true
exl-id: eeb0d39d-58a4-4414-9123-2cf1b27b73de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 도메인 서버 설정{#set-up-a-domain-server}

기존 라이센스 서버 설치에서 도메인 서버를 구성하려면 다음을 수행합니다.

1. 다음에서 [!DNL tomcat/lib] 디렉토리, 열기 [!DNL flashaccess-refimpl.properties] 파일.
1. 아래 `Domain CA certificate` 도메인 CA 인증서를 완료합니다.

   그런 다음 이 인증서는 도메인 토큰을 수락하는 데 사용됩니다.
1. 아래 `Domain CA credential` 옵션, 완료 `Domain CA credential certificate (PFX)` 세부 정보.

   그런 다음 이 인증서는 도메인 인증서 및 토큰에 서명하는 데 사용됩니다.
1. 다음에 대한 값 지정 `DomainServerlURL`.

   이 값이 로 설정된 경우 `NULL`, 도메인 인증이 성공할 수 있습니다. 그러나 도메인에 가입하는 동안 도메인 가입 오류가 발생할 수 있습니다.
