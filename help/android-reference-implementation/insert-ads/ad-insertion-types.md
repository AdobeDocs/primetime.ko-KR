---
description: TVSDK는 현재 TV SDK 광고, DMB 광고, DM(Direct Ad Break) 및 맞춤형 광고 마커에 대한 내장된 광고 공급업체 메타데이터 지원을 제공하고 있습니다.
title: 광고 삽입 유형
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 광고 삽입 유형 {#ad-insertion-types}

TVSDK는 현재 TV SDK 광고, DMB 광고, DM(Direct Ad Break) 및 맞춤형 광고 마커에 대한 내장된 광고 공급업체 메타데이터 지원을 제공하고 있습니다.

VOD 및 라이브/선형 컨텐츠에 대해 다음과 같은 유형의 광고 삽입 워크플로우를 지원합니다.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 삽입 유형 </th> 
   <th colname="col2" class="entry"> 지원 대상... </th> 
   <th colname="col3" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Adobe Primetime 광고 결정 광고 </td> 
   <td colname="col2">VOD <p>라이브 </p> <p>선형 </p> </td> 
   <td colname="col3">참조 구현에서는 JSON 구성 파일</a>의 Primetime 광고 부분</a>에 제공된 정보를 기반으로, Primetime 광고 결정(이전의 Auditude)을 위한 서버에 연결하는 <span class="codeph"> AuditudeMetadata</span> 정보를 제공합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 직접 광고 나누기 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">입력 JSON 파일에 광고 URL을 제공해야 합니다. TVSDK가 광고 해결을 시도할 때 직접 광고 차단 프로그램을 호출하고 JSON 구성 파일</a>에 제공된 직접 광고 나누기 정보를 기반으로 광고를 해결합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 사용자 정의 광고 마커 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">사용자 지정 광고 마커는 비디오 스트림에 기본 컨텐츠와 광고가 모두 포함되지만 광고 위치 및 타이밍과 관련된 정보는 포함되지 않을 때 유용합니다. 예를 들어 외부 CMS를 통해 광고 위치 정보를 다른 방법으로 얻을 경우 사용자 지정 광고 마커를 정의하여 플레이어 타임라인으로 전달할 수 있습니다. <p>광고 삽입용 플레이어를 설정하려면 참조 구현에서 지원 광고 공급자 구현이 있는 JSON 구성 파일</a>의 사용자 지정 광고 메타데이터 섹션에 광고 메타데이터를 전달해야 합니다. </p> </td>
  </tr>
 </tbody>
</table>