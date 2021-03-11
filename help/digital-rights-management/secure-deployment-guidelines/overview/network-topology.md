---
title: 네트워크 토폴로지 개요
description: 네트워크 토폴로지 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 개요 {#network-topology-overview}

Adobe Primetime DRM을 성공적으로 배포한 후 Primetime DRM 프로덕션 서버의 보안을 유지해야 합니다.

>[!NOTE]
>
>Primetime DRM은 이전에 Adobe 액세스으로 알려졌고 그 이전에는 Flash Access이었습니다.

*역방향 프록시*&#x200B;을 사용하여 Primetime DRM 웹 응용 프로그램의 다른 URL 세트를 외부 및 내부 사용자가 사용할 수 있도록 할 수 있습니다. *Primetime* DRM이 실행되는 응용 프로그램 서버에 사용자가 직접 연결할 수 있고 이 구성은 Primetime DRM을 실행하는 응용 프로그램 서버에 대한 모든 HTTP 요청을 수행하는 것보다 더 안전합니다. 사용자는 역방향 프록시에만 액세스할 수 있고 역방향 프록시에서 지원되는 URL 연결만 시도할 수 있습니다.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)