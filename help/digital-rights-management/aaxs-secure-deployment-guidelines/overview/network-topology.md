---
title: 네트워크 토폴로지 개요
description: 네트워크 토폴로지 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 네트워크 토폴로지 개요 {#network-topology-overview}

Adobe 액세스를 성공적으로 배포한 후에는 환경의 보안을 유지하는 것이 중요합니다. 이 섹션에서는 Adobe 액세스 프로덕션 서버의 보안을 유지하는 데 필요한 작업에 대해 설명합니다.

Adobe 액세스 웹 응용 프로그램에 대해 다른 URL 세트를 외부 및 내부 사용자 모두 사용할 수 있도록 하려면 *역방향 프록시*&#x200B;을 사용합니다. 이 구성은 Adobe 액세스가 실행 중인 응용 프로그램 서버에 사용자가 직접 연결할 수 있도록 하는 것보다 더 안전합니다. 역방향 프록시는 Adobe 액세스를 실행 중인 응용 프로그램 서버에 대한 모든 HTTP 요청을 수행합니다. 사용자는 역방향 프록시에 대한 네트워크 액세스 권한만 가지며 역방향 프록시에서 지원되는 URL 연결만 시도할 수 있습니다.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

