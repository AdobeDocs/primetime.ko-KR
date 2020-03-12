---
seo-title: 네트워크 토폴로지 개요
title: 네트워크 토폴로지 개요
uuid: b8b072dc-8dc0-46ba-bb01-1e9b58af2681
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 개요 {#network-topology-overview}

Adobe Primetime DRM을 성공적으로 배포한 후에는 Primetime DRM 프로덕션 서버의 보안을 유지해야 합니다.

>[!NOTE]
>
>Primetime DRM은 이전에 Adobe Access로 알려졌고 그 이전인 Flash Access로 이름이 바뀌었습니다.

역방향 프록시를 ** 사용하여 Primetime DRM 웹 응용 프로그램에 대해 다른 URL 세트를 외부 및 내부 사용자가 사용할 수 있도록 할 수 있습니다. *역방향 프록시는* 사용자가 Primetime DRM이 실행되는 응용 프로그램 서버에 직접 연결할 수 있게 하는 것보다 더 안전하며, 이 구성은 Primetime DRM을 실행하는 응용 프로그램 서버에 대한 모든 HTTP 요청을 수행합니다. 사용자는 역방향 프록시에만 액세스할 수 있으며 역방향 프록시에서 지원하는 URL 연결만 시도할 수 있습니다.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)