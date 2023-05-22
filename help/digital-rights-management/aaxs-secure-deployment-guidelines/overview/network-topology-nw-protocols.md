---
title: Adobe 액세스에서 사용하는 네트워크 프로토콜
description: Adobe 액세스에서 사용하는 네트워크 프로토콜
copied-description: true
exl-id: f065690d-6fa1-43a7-8aa8-a1ccd68e998d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Adobe 액세스에서 사용하는 네트워크 프로토콜 {#network-protocols-used-by-adobe-access}

보안 네트워크 아키텍처를 구성할 때 다음 표의 네트워크 프로토콜은 Adobe 액세스와 엔터프라이즈 네트워크의 다른 시스템 간의 상호 작용에 필요합니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">프로토콜 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">사용 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player , Adobe AIR® 및 Adobe Primetime 클라이언트는 HTTP를 통해 Adobe 액세스와 통신합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS(선택 사항) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR 및 Adobe Primetime 클라이언트는 Adobe 액세스와의 통신에 HTTPS를 사용할 수 있지만 FMRMS 1.x 클라이언트에 대한 지원이 필요하지 않으면 HTTPS(SSL)가 필요하지 않습니다. 표에 있는 참고 사항 보기 <a href="network-topology-firewall-rules.md" format="dita" scope="local"> 수신 URL</a> 및 <a href="network-topology-nw-protocols.md"> SSL 구성</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
