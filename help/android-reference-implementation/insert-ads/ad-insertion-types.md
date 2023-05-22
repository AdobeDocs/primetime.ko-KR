---
description: TVSDK는 현재 TVSDK 광고, 직접 광고 브레이크 및 사용자 지정 광고 마커에 대한 기본 제공 광고 공급자 메타데이터 지원을 제공합니다.
title: 광고 삽입 유형
exl-id: 1634ff41-8a8f-4f34-9685-149ec58518ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 광고 삽입 유형 {#ad-insertion-types}

TVSDK는 현재 TVSDK 광고, 직접 광고 브레이크 및 사용자 지정 광고 마커에 대한 기본 제공 광고 공급자 메타데이터 지원을 제공합니다.

VOD 및 라이브/선형 컨텐츠에 대한 다음 유형의 광고 삽입 워크플로우를 지원합니다.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 삽입 유형 </th> 
   <th colname="col2" class="entry"> 지원 위치... </th> 
   <th colname="col3" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Adobe Primetime ad decisioning 광고 </td> 
   <td colname="col2">VOD <p>라이브 </p> <p>선형 </p> </td> 
   <td colname="col3">참조 구현은 다음을 제공합니다 <span class="codeph"> AuditudeMetadata</span> Primetime 광고 부분에 제공된 정보를 기반으로 Primetime 광고 의사 결정(이전 이름: Auditude)을 위해 서버에 연결하는 정보</a> / JSON 구성 파일</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 직접 광고 브레이크 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">입력 JSON 파일에 광고 URL을 제공해야 합니다. TVSDK에서 광고를 확인하려고 하면 직접 광고 브레이크 해결자를 호출하고 JSON 구성 파일에 제공된 직접 광고 브레이크 정보를 기반으로 광고를 확인합니다</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 사용자 지정 광고 마커 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">사용자 지정 광고 마커는 비디오 스트림에 기본 컨텐츠와 광고가 모두 포함되어 있지만 광고 위치 및 타이밍과 관련된 정보가 포함되어 있지 않은 경우에 유용합니다. 광고 위치 지정 정보를 다른 방법(예: 외부 CMS를 통해 획득)으로 가져오는 경우 사용자 지정 광고 마커를 정의하고 이를 플레이어 타임라인에 전달할 수 있습니다. <p>광고 삽입용 플레이어를 설정하려면 JSON 구성 파일의 사용자 지정 광고 메타데이터 섹션에 광고 메타데이터를 전달해야 합니다</a>참조 구현에 지원 광고 공급자 구현이 있는 . </p> </td>
  </tr>
 </tbody>
</table>
