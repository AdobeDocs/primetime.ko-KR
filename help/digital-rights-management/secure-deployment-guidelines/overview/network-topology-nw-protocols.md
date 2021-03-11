---
description: 보안 네트워크 아키텍처를 구성할 때 네트워크 프로토콜은 기업 네트워크의 Adobe Primetime DRM과 다른 시스템 간의 상호 작용을 위해 필요합니다.
title: Adobe Primetime DRM 네트워크 프로토콜
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Adobe Primetime DRM 네트워크 프로토콜 {#adobe-primetime-drm-network-protocols}

보안 네트워크 아키텍처를 구성할 때 네트워크 프로토콜은 기업 네트워크의 Adobe Primetime DRM과 다른 시스템 간의 상호 작용을 위해 필요합니다.

보안 네트워크 아키텍처를 구성할 때 이러한 상호 작용에 다음과 같은 네트워크 프로토콜이 필요합니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">프로토콜 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">사용 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR® 및 Adobe Primetime 클라이언트는 HTTP를 통해 Primetime DRM과 통신합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS(선택 사항) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR 및 Adobe Primetime 클라이언트는 HTTPS를 사용하여 Primetime DRM과 통신할 수 있습니다.FMRMS 1.x 클라이언트를 지원하지 않는 경우 HTTPS(SSL)가 필요하지 않습니다. 자세한 내용은 <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> 수신 URL </a> 및 SSL 구성을 참조하십시오. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 응용 프로그램 서버용 포트 {#ports-for-application-servers}

모든 네트워크 포트를 사용하도록 Adobe Primetime DRM 라이선스 서버를 구성할 수 있습니다.

Primetime DRM을 실행하는 응용 프로그램 서버에 연결하는 클라이언트를 허용하려는 네트워크 기능에 따라, 내부 방화벽에서 이 포트를 활성화하거나 비활성화해야 합니다.

## SSL {#configuring-ssl} 구성

SSL(Secure Sockets Layer)은 Flash Media Library Server 1.x 클라이언트에 대한 지원이 필요한 경우에만 필요합니다.

Adobe Primetime DRM 키 서버에 클라이언트 인증을 사용하는 SSL이 필요합니다. 자세한 내용은 [Adobe Primetime DRM 키 서버 사용](../../using-the-drm-key-server/requirements.md)을 참조하십시오.