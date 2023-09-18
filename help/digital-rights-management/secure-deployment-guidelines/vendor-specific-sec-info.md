---
description: 운영 체제와 애플리케이션 서버는 Adobe Primetime DRM 솔루션에 포함되어 있습니다.
title: 공급업체별 보안 정보
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 공급업체별 보안 정보{#vendor-specific-security-information}

운영 체제와 애플리케이션 서버는 Adobe Primetime DRM 솔루션에 포함되어 있습니다.

운영 체제 및 애플리케이션 서버에 대한 공급업체별 보안 정보를 찾으려면 Adobe Primetime DRM 키 서버 사용을 참조하십시오.

## 운영 체제 보안 정보 {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

운영 체제를 보호할 때는 운영 체제 공급업체에서 설명한 조치를 이행해야 합니다.

다음은 몇 가지 조치입니다.

* 사용자, 롤 및 권한 정의 및 제어
* 로그 및 감사 추적 모니터링
* 불필요한 서비스 및 응용 프로그램 제거
* 파일 백업

다음은 Adobe Primetime DRM에서 지원하는 운영 체제에 대한 정보입니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">운영 체제 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">보안 리소스 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise 또는 Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Windows Server 2008 보안 안내서</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 및 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5 Security 안내서</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

다음은 운영 체제의 보안 취약점을 최소화하는 방법에 대한 정보입니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">항목 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">보안 패치 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">공급업체 보안 패치 및 업그레이드가 적시에 적용되지 않을 경우 권한이 없는 사용자가 애플리케이션 서버에 액세스할 수 있는 위험이 증가합니다. </p> <p>참고: 프로덕션 서버에 적용하기 전에 보안 패치를 테스트하십시오. </p> <p class="- topic/p ">패치를 정기적으로 확인하고 설치하려면 정책 및 절차를 만들어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">바이러스 보호 소프트웨어 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">바이러스 스캐너는 서명 또는 비정상적인 행동을 스캔하여 감염된 파일을 식별할 수 있습니다. </p> <p>스캐너는 보통 로컬 하드 드라이브에 저장되어 있는 파일에 바이러스 서명을 보관합니다. 새로운 바이러스가 자주 발견되므로 이 파일이 정기적으로 업데이트되는지 확인해야 합니다. 이러한 방식으로, 바이러스 스캐너는 항상 모든 현재 바이러스를 식별할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP(Network Time Protocol) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">적절한 작동 및 포렌식 분석을 위해 Primetime DRM 서버 및 패키지에서 정확한 시간을 유지합니다. 인터넷에 연결된 모든 시스템에서 보안 버전의 NTP를 사용하여 Primetime DRM 시간을 동기화합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 응용 프로그램 서버 보안 정보 {#section_22986936F1A547CEAB2D97E9E9D4825C}

애플리케이션 서버의 보안을 설정할 때는 서버 공급업체에서 설명한 방법을 구현해야 합니다.

다음은 이러한 조치 중 일부입니다.

* 명확하지 않은 관리자 사용자 이름 사용
* 불필요한 서비스 비활성화
* 콘솔 관리자 보호
* 보안 쿠키 활성화
* 불필요한 포트 닫기
* IP 주소 또는 도메인별로 관리 인터페이스 제한
* Java™ Security Manager 사용
