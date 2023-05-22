---
title: 공급업체별 보안 정보
description: 공급업체별 보안 정보
copied-description: true
exl-id: 668321c5-b2c7-4bb3-9f68-2dba622a54de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 공급업체별 보안 정보{#vendor-specific-security-information}

이 섹션에는 Adobe 액세스 솔루션에 통합된 운영 체제 및 애플리케이션 서버에 대한 보안 관련 정보가 포함되어 있습니다.

이 섹션에 제공된 링크를 사용하여 운영 체제 및 애플리케이션 서버에 대한 공급업체별 보안 정보를 찾으십시오.

## 운영 체제 보안 정보 {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

운영 체제를 보호할 때는 다음을 포함하여 운영 체제 공급업체에서 설명한 조치를 신중하게 구현합니다.

* 사용자, 롤 및 권한 정의 및 제어
* 로그 및 감사 추적 모니터링
* 불필요한 서비스 및 응용 프로그램 제거
* 파일 백업

Adobe 액세스가 지원하는 운영 체제에 대한 보안 정보는 이 표의 리소스를 참조하십시오.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
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

다음 표에서는 운영 체제에서 발견되는 보안 취약성을 최소화하기 위한 몇 가지 잠재적인 접근 방식에 대해 설명합니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">항목 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">보안 패치 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">공급업체 보안 패치 및 업그레이드가 적시에 적용되지 않을 경우 권한이 없는 사용자가 애플리케이션 서버에 액세스할 수 있는 위험이 증가합니다. 보안 패치를 프로덕션 서버에 적용하기 전에 테스트합니다. </p> <p class="- topic/p ">또한 규칙적으로 패치를 확인하고 설치하는 정책 및 절차를 만듭니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">바이러스 보호 소프트웨어 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">바이러스 스캐너는 서명을 스캔하거나 비정상적인 행동을 관찰하여 감염된 파일을 식별할 수 있습니다. 스캐너는 보통 로컬 하드 드라이브에 저장되어 있는 파일에 바이러스 서명을 보관합니다. 새 바이러스가 자주 발견되므로 바이러스 검사 프로그램이 현재 바이러스를 모두 식별하려면 이 파일을 자주 업데이트해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP(Network Time Protocol) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">적절한 운영과 법정 분석을 위해 Adobe 액세스 서버와 Adobe 액세스 패키지에서 정확한 시간을 유지합니다. 보안 버전의 NTP를 사용하여 인터넷에 연결된 모든 시스템의 시간을 동기화합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 응용 프로그램 서버 보안 정보 {#section-EBB4EF371CFF4A848694CC240B23D404}

애플리케이션 서버의 보안을 설정할 때 다음과 같은 서버 공급업체에서 설명하는 조치를 구현해야 합니다.

* 명확하지 않은 관리자 사용자 이름 사용
* 불필요한 서비스 비활성화
* 콘솔 관리자 보호
* 보안 쿠키 활성화
* 불필요한 포트 닫기
* IP 주소 또는 도메인별로 관리 인터페이스 제한
* Java™ Security Manager 사용
