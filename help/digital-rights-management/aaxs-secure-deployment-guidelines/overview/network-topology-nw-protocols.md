---
seo-title: Adobe Access에서 사용하는 네트워크 프로토콜
title: Adobe Access에서 사용하는 네트워크 프로토콜
uuid: 4f2ee3f5-6758-4fbe-b5cd-cead1e5ccde8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Adobe Access에서 사용하는 네트워크 프로토콜 {#network-protocols-used-by-adobe-access}

보안 네트워크 아키텍처를 구성할 때 다음 표의 네트워크 프로토콜은 Adobe Access와 엔터프라이즈 네트워크의 다른 시스템 간의 상호 작용을 위해 필요합니다.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR® 및 Adobe Primetime 클라이언트는 HTTP를 통해 Adobe Access와 통신합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS(선택 사항) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR 및 Adobe Primetime 클라이언트는 HTTPS를 사용하여 Adobe Access와 통신할 수 있지만 FMRMS 1.x 클라이언트에 대한 지원이 필요하지 않은 경우 HTTPS(SSL)가 필요하지 않습니다. 수신 URL 및 SSL 구성 <a href="network-topology-firewall-rules.md" format="dita" scope="local"> 테이블의</a> 메모를 <a href="network-topology-nw-protocols.md"> 참조하십시오</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>