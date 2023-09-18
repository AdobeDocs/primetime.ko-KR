---
description: 네트워크 보안 취약성은 인터넷 연결 또는 인트라넷 연결 응용 프로그램 서버에 대한 첫 번째 위협 중 하나이며 이러한 취약점에 대비하여 네트워크의 호스트를 강화해야 합니다.
title: 네트워크 계층 보안
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 네트워크 계층 보안{#network-layer-security}

네트워크 보안 취약성은 인터넷 연결 또는 인트라넷 연결 응용 프로그램 서버에 대한 첫 번째 위협 중 하나이며 이러한 취약점에 대비하여 네트워크의 호스트를 강화해야 합니다.

다음은 네트워크 보안 취약성을 줄이는 몇 가지 일반적인 기술입니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">기법 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">비무장 지대(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">세그먼테이션은 Primetime DRM이 내부 방화벽 뒤에 있을 때 Adobe Primetime DRM을 실행하는 데 사용되는 애플리케이션 서버와 최소 두 개 수준에 있어야 합니다. 웹 서버를 포함하는 DMZ에서 외부 네트워크를 분리해야 하며 웹 서버는 내부 네트워크에서 분리해야 합니다. 방화벽을 사용하여 이러한 분리 레이어를 구현할 수 있습니다. </p> <p>필요한 데이터의 절대 최소값만 허용되도록 각 네트워크 계층을 통과하는 트래픽을 분류하고 제어할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">비공개 IP 주소 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Primetime DRM 애플리케이션 서버에서 RFC 1918 개인 IP 주소와 함께 NAT(Network Address Translation)를 사용하십시오. 개인 IP 주소(10.0.0.0/8, 172.16.0.0/12 및 192.168.0.0/16)를 할당하여 공격자가 인터넷을 통해 NAT 내부 호스트로/에서 트래픽을 라우팅하는 것을 더 어렵게 할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">방화벽 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">다음은 방화벽 솔루션을 선택할 때 고려해야 할 몇 가지 기준입니다. </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">간단한 패킷 필터링 솔루션 대신 프록시 서버 및/또는 상태 저장 검사를 지원하는 방화벽을 구현합니다. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">명시적으로 허용된 서비스를 제외한 모든 서비스를 거부할 수 있는 보안 패러다임을 지원하는 방화벽을 사용합니다. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">이중 홈 또는 다중 홈 방화벽 솔루션 구현 이 아키텍처는 가장 높은 수준의 보안을 제공하고 승인되지 않은 사용자가 방화벽 보안을 우회하지 못하도록 합니다. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
