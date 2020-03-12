---
description: 보안 네트워크 아키텍처를 구성할 때 Adobe Primetime DRM과 엔터프라이즈 네트워크의 다른 시스템 간의 상호 작용을 위해 네트워크 프로토콜이 필요합니다.
seo-description: 보안 네트워크 아키텍처를 구성할 때 Adobe Primetime DRM과 엔터프라이즈 네트워크의 다른 시스템 간의 상호 작용을 위해 네트워크 프로토콜이 필요합니다.
seo-title: Adobe Primetime DRM 네트워크 프로토콜
title: Adobe Primetime DRM 네트워크 프로토콜
uuid: 8954e33c-83ac-4b40-9e45-005d4954b44e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Adobe Primetime DRM 네트워크 프로토콜 {#adobe-primetime-drm-network-protocols}

보안 네트워크 아키텍처를 구성할 때 Adobe Primetime DRM과 엔터프라이즈 네트워크의 다른 시스템 간의 상호 작용을 위해 네트워크 프로토콜이 필요합니다.

보안 네트워크 아키텍처를 구성할 때 이러한 상호 작용에 대해 다음 네트워크 프로토콜이 필요합니다.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR® 및 Adobe Primetime 클라이언트는 HTTP 파섹 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS(선택 사항) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR 및 Adobe Primetime 클라이언트는 HTTPS를 사용하여 Primetime DRM과 통신할 수 있습니다.FMRMS 1.x 클라이언트를 지원하지 않는 경우 HTTPS(SSL)가 필요하지 않습니다. 자세한 내용은 들어오는 URL <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> 및 SSL 구성을 </a> 참조하십시오. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 애플리케이션 서버용 포트 {#ports-for-application-servers}

Adobe Primetime DRM 라이선스 서버를 네트워크 포트를 사용하도록 구성할 수 있습니다.

Primetime DRM을 실행하는 응용 프로그램 서버에 연결할 클라이언트에 대해 허용할 네트워크 기능에 따라 이러한 포트를 내부 방화벽에서 활성화하거나 비활성화해야 합니다.

## SSL 구성 {#configuring-ssl}

SSL(Secure Sockets Layer)은 Flash Media Rights Management Server 1.x 클라이언트에 대한 지원이 필요한 경우에만 필요합니다.

Adobe Primetime DRM 키 서버에 클라이언트 인증이 있는 SSL이 필요합니다. 자세한 내용은 Adobe Primetime [DRM 키 서버 사용을 참조하십시오](../../using-the-drm-key-server/requirements.md).