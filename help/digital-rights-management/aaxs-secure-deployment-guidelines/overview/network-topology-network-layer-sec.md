---
title: 네트워크 계층 보안
description: 네트워크 계층 보안
copied-description: true
exl-id: 70c9917d-32bc-43f6-add3-62883f98ac5e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 네트워크 계층 보안{#network-layer-security}

네트워크 보안 취약성은 모든 인터넷 연결 또는 인트라넷 연결 응용 프로그램 서버에 가장 먼저 위협됩니다. 이 섹션에서는 이러한 취약점에 대해 네트워크의 호스트를 강화하는 프로세스에 대해 설명합니다. 네트워크 세그멘테이션, TCP/IP(Transmission Control Protocol/Internet Protocol) 스택 강화 및 호스트 보호를 위한 방화벽 사용을 해결합니다.

이 표에서는 네트워크 보안 취약성을 줄이는 일반적인 기술에 대해 설명합니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">기법 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">비무장 지대(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">내부 방화벽 뒤에 배치된 Adobe 액세스를 실행하는 데 사용되는 애플리케이션 서버에는 세그먼테이션이 두 개 이상의 수준에 있어야 합니다. 웹 서버를 포함하는 DMZ에서 외부 네트워크를 분리하여 내부 네트워크와 분리해야 합니다. 방화벽을 사용하여 분리 레이어를 구현합니다. 각 네트워크 계층을 통과하는 트래픽을 분류하고 제어하여 필요한 데이터의 절대 최소값만 허용되도록 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">비공개 IP 주소 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adobe 액세스 애플리케이션 서버에서 RFC 1918 개인 IP 주소와 함께 NAT(Network Address Translation)를 사용하십시오. 공격자가 인터넷을 통해 NAT 내부 호스트로/에서 트래픽을 라우팅하는 것을 더 어렵게 하려면 개인 IP 주소(10.0.0.0/8, 172.16.0.0/12 및 192.168.0.0/16)를 할당하십시오. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">방화벽 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">다음 기준을 사용하여 방화벽 솔루션을 선택합니다. </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">간단한 패킷 필터링 솔루션 대신 프록시 서버 및/또는 상태 저장 검사를 지원하는 방화벽을 구현합니다. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">명시적으로 허용된 서비스를 제외한 모든 서비스를 거부할 수 있는 보안 패러다임을 지원하는 방화벽을 사용합니다. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">이중 홈 또는 다중 홈 방화벽 솔루션 구현 이 아키텍처는 가장 높은 수준의 보안을 제공하고 승인되지 않은 사용자가 방화벽 보안을 무시하는 것을 방지합니다. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
