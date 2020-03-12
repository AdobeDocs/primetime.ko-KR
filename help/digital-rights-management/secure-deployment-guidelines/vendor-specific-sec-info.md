---
description: Adobe Primetime DRM 솔루션에 운영 체제와 애플리케이션 서버가 포함되어 있습니다.
seo-description: Adobe Primetime DRM 솔루션에 운영 체제와 애플리케이션 서버가 포함되어 있습니다.
seo-title: 공급업체별 보안 정보
title: 공급업체별 보안 정보
uuid: 331baa42-5e19-40a5-bc74-0b1a2cb9370e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 공급업체별 보안 정보{#vendor-specific-security-information}

Adobe Primetime DRM 솔루션에 운영 체제와 애플리케이션 서버가 포함되어 있습니다.

운영 체제 및 응용 프로그램 서버에 대한 공급업체별 보안 정보를 찾으려면 Adobe Primetime DRM 키 서버 사용을 참조하십시오.

## 운영 체제 보안 정보 {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

운영 체제의 보안을 유지하는 경우 운영 체제 공급업체에서 설명하는 조치를 구현해야 합니다.

다음은 몇 가지 방법입니다.

* 사용자, 역할 및 권한 정의 및 제어
* 로그 및 감사 추적 모니터링
* 불필요한 서비스 및 애플리케이션 제거
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
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5 보안 가이드</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

다음은 운영 체제의 보안 취약점을 최소화하는 접근 방법에 대한 정보입니다.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">벤더 보안 패치와 업그레이드가 시기 적절하게 적용되지 않는 경우 인증되지 않은 사용자가 애플리케이션 서버에 액세스할 수 있는 위험이 높아집니다. </p> <p>참고: 보안 패치를 프로덕션 서버에 적용하기 전에 테스트해야 합니다. </p> <p class="- topic/p ">패치를 정기적으로 확인하고 설치할 정책과 절차를 생성해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">바이러스 보호 소프트웨어 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">바이러스 스캐너는 서명 또는 비정상적인 동작을 스캔하여 감염된 파일을 식별할 수 있습니다. </p> <p>스캐너는 바이러스 서명을 파일에 보관합니다. 파일은 일반적으로 로컬 하드 드라이브에 저장됩니다. 새로운 바이러스가 자주 발견되므로 이 파일이 정기적으로 업데이트되도록 해야 합니다. 이렇게 하면 바이러스 스캐너는 항상 모든 최신 바이러스를 찾아낼 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP(Network Time Protocol) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">적절한 운영 및 법의학 분석을 위해 Primetime DRM 서버 및 패키저에서 시간을 정확하게 관리할 수 있습니다. NTP의 보안 버전을 사용하여 인터넷에 연결된 모든 시스템에서 Primetime DRM 시간을 동기화할 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 응용 프로그램 서버 보안 정보 {#section_22986936F1A547CEAB2D97E9E9D4825C}

응용 프로그램 서버의 보안을 유지하는 경우 서버 공급업체에서 설명하는 조치를 구현해야 합니다.

다음은 몇 가지 방법입니다.

* 분명하지 않은 관리자 사용자 이름 사용
* 불필요한 서비스 비활성화
* 콘솔 관리자 보안
* 보안 쿠키 활성화
* 불필요한 포트를 닫는 중
* IP 주소 또는 도메인별로 관리 인터페이스 제한
* Java™ Security Manager 사용

