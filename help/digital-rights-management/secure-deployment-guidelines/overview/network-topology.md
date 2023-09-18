---
title: 네트워크 토폴로지 개요
description: 네트워크 토폴로지 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 개요 {#network-topology-overview}

Adobe Primetime DRM을 성공적으로 배포한 후에는 Primetime DRM 프로덕션 서버의 보안을 유지해야 합니다.

>[!NOTE]
>
>Primetime DRM은 이전에 Adobe 액세스라고 했으며 그 이전에는 Flash Access라고 했습니다.

다음을 사용할 수 있습니다. *역방향 프록시* 외부 및 내부 사용자가 Primetime DRM 웹 애플리케이션의 다양한 URL 세트를 사용할 수 있도록 하기 위해 *역방향 프록시* 는 사용자가 Primetime DRM이 실행되는 애플리케이션 서버에 직접 연결할 수 있는 것보다 안전하며, 이 구성은 Primetime DRM을 실행하는 애플리케이션 서버에 대한 모든 HTTP 요청을 수행합니다. 사용자는 역방향 프록시에만 액세스할 수 있으며 역방향 프록시에서 지원하는 URL 연결만 시도할 수 있습니다.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
