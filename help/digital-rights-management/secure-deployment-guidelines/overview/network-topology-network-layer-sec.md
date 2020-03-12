---
description: 네트워크 보안 취약점은 인터넷 연결 또는 인트라넷 기반 응용 프로그램 서버에 대한 첫 번째 위협 중 하나이며, 이러한 취약점에 대해 네트워크에 대한 호스트를 보호해야 합니다.
seo-description: 네트워크 보안 취약점은 인터넷 연결 또는 인트라넷 기반 응용 프로그램 서버에 대한 첫 번째 위협 중 하나이며, 이러한 취약점에 대해 네트워크에 대한 호스트를 보호해야 합니다.
seo-title: 네트워크 레이어 보안
title: 네트워크 레이어 보안
uuid: c750c595-a784-47ce-be0b-17b8d60c5753
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 네트워크 레이어 보안{#network-layer-security}

네트워크 보안 취약점은 인터넷 연결 또는 인트라넷 기반 응용 프로그램 서버에 대한 첫 번째 위협 중 하나이며, 이러한 취약점에 대해 네트워크에 대한 호스트를 보호해야 합니다.

다음은 네트워크 보안 취약점을 줄이는 몇 가지 일반적인 기술입니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">기법 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">비무장지대(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Primetime DRM이 내부 방화벽 뒤에 있을 때 Adobe Primetime DRM을 실행하는 데 사용되는 애플리케이션 서버가 있는 세그먼테이션은 최소 2개 수준에 있어야 합니다. 외부 네트워크를 웹 서버를 포함하는 DMZ에서 분리해야 하며 웹 서버는 내부 네트워크에서 분리되어야 합니다. 방화벽을 사용하여 이러한 분판 레이어를 구현할 수 있습니다. </p> <p>각 네트워크 레이어를 통과하는 트래픽을 분류하고 제어하여 필요한 데이터의 절대 최소값만 허용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">개인 IP 주소 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Primetime DRM 애플리케이션 서버에서 RFC 1918 개인 IP 주소와 함께 NAT(네트워크 주소 변환)를 사용합니다. 비공개 IP 주소(10.0.0.0/8, 172.16.0.0/12 및 192.168.0.0/16)을 할당하여 침입자가 인터넷을 통해 NAT 내부 호스트에 트래픽을 라우팅하는 것을 더욱 어렵게 만들 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">방화벽 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">다음은 방화벽 솔루션을 선택할 때 고려해야 할 몇 가지 사항입니다. </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">단순 패킷 필터링 솔루션 대신 프록시 서버 및/또는 상태 저장 검사를 지원하는 방화벽을 구현합니다. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">명시적으로 허용된 서비스를 제외한 모든 서비스를 거부할 수 있는 보안 패러다임을 지원하는 방화벽을 사용하십시오. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">이중 홈 또는 다중 홈인 방화벽 솔루션을 구현합니다. 이 아키텍처는 최고 수준의 보안을 제공하며 권한이 없는 사용자가 방화벽 보안을 우회하지 못하도록 합니다. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

