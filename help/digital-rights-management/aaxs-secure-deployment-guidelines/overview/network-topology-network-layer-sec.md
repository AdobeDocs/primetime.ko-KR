---
seo-title: 네트워크 레이어 보안
title: 네트워크 레이어 보안
uuid: bd53bccf-1130-4189-97ec-4259bd25762f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 네트워크 레이어 보안{#network-layer-security}

네트워크 보안 취약점은 인터넷 접속 또는 인트라넷 기반 애플리케이션 서버에 대한 첫 번째 위협 중 하나입니다. 이 섹션에서는 이러한 취약점에 대한 네트워크의 호스트 강화 프로세스에 대해 설명합니다. 네트워크 세분화, TCP/IP(Transmission Control Protocol/Internet Protocol) 스택 보강 및 호스트 보호를 위한 방화벽 사용에 대해 다룹니다.

이 표에서는 네트워크 보안 취약점을 줄이는 일반적인 기술에 대해 설명합니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">기법 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">비무장지대(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">세그멘테이션은 내부 방화벽 뒤에 있는 Adobe 액세스를 실행하는 데 사용되는 응용 프로그램 서버와 함께 두 개 이상의 수준에 있어야 합니다. 웹 서버가 포함된 DMZ에서 외부 네트워크를 분리하고 내부 네트워크에서 분리해야 합니다. 방화벽을 사용하여 분판 레이어를 구현합니다. 각 네트워크 레이어를 통과하는 트래픽을 분류하고 제어하여 필요한 데이터의 절대 최소값만 허용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">개인 IP 주소 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adobe 액세스 응용 프로그램 서버에서 RFC 1918 개인 IP 주소에 NAT(네트워크 주소 변환)를 사용하십시오. 비공개 IP 주소(10.0.0.0/8, 172.16.0.0/12 및 192.168.0.0/16)을 할당하여 공격자가 인터넷을 통해 NAT 내부 호스트에 트래픽을 라우팅하는 것을 더욱 어렵게 만듭니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">방화벽 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">방화벽 솔루션을 선택하려면 다음 기준을 사용하십시오. </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">단순 패킷 필터링 솔루션 대신 프록시 서버 및/또는 상태 저장 검사를 지원하는 방화벽을 구현합니다. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">명시적으로 허용된 서비스를 제외한 모든 서비스를 거부할 수 있는 보안 패러다임을 지원하는 방화벽을 사용하십시오. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">이중 홈 또는 다중 홈인 방화벽 솔루션을 구현합니다. 이 아키텍처는 최고 수준의 보안 기능을 제공하며 권한이 없는 사용자가 방화벽 보안을 우회하지 못하도록 합니다. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

