---
seo-title: 네트워크 토폴로지 개요
title: 네트워크 토폴로지 개요
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 네트워크 토폴로지 개요 {#network-topology-overview}

Adobe Access를 성공적으로 배포한 후에는 환경의 보안을 유지하는 것이 중요합니다. 이 섹션에서는 Adobe Access 프로덕션 서버의 보안을 유지하는 데 필요한 작업에 대해 설명합니다.

역방향 *프록시를* 사용하여 Adobe Access 웹 응용 프로그램에 대한 다양한 URL 집합을 외부 사용자와 내부 사용자 모두 사용할 수 있도록 합니다. 이 구성은 사용자가 Adobe Access가 실행 중인 응용 프로그램 서버에 직접 연결할 수 있도록 하는 것보다 더 안전합니다. 역방향 프록시는 Adobe Access를 실행 중인 응용 프로그램 서버에 대한 모든 HTTP 요청을 수행합니다. 사용자는 역방향 프록시에 대한 네트워크 액세스 권한만 가지며 역방향 프록시에서 지원하는 URL 연결만 시도할 수 있습니다.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

