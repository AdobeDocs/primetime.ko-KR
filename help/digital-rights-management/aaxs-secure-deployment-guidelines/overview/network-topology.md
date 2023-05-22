---
title: 네트워크 토폴로지 개요
description: 네트워크 토폴로지 개요
copied-description: true
exl-id: ca5e8701-f8a3-4125-bb60-bfb9efd5c8f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# 네트워크 토폴로지 개요 {#network-topology-overview}

Adobe 액세스를 성공적으로 배포한 후에는 환경 보안을 유지하는 것이 중요합니다. 이 섹션에서는 Adobe 액세스 프로덕션 서버의 보안을 유지하는 데 필요한 작업에 대해 설명합니다.

사용 *역방향 프록시* 외부 사용자와 내부 사용자가 Adobe 액세스 웹 응용 프로그램에 대해 서로 다른 URL 집합을 사용할 수 있도록 합니다. 이 구성은 사용자가 Adobe 액세스가 실행 중인 애플리케이션 서버에 직접 연결할 수 있는 것보다 더 안전합니다. 역방향 프록시는 Adobe 액세스를 실행 중인 응용 프로그램 서버에 대한 모든 HTTP 요청을 수행합니다. 사용자는 역방향 프록시에 대한 네트워크 액세스 권한만 가지며 역방향 프록시에서 지원하는 URL 연결만 시도할 수 있습니다.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)
