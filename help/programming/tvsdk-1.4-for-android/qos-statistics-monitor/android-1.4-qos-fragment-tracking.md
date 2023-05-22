---
description: QoS(서비스 품질)는 비디오 엔진이 수행되는 방식에 대한 세부 보기를 제공합니다. TVSDK는 재생, 버퍼링 및 장치에 대한 자세한 통계를 제공합니다.
title: 로드 정보를 사용하여 조각 수준에서 추적
exl-id: 29e82a93-783f-4e32-ab5e-12713a60cfec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 로드 정보를 사용하여 조각 수준에서 추적{#track-at-the-fragment-level-using-load-information}

QoS(서비스 품질)는 비디오 엔진이 수행되는 방식에 대한 세부 보기를 제공합니다. TVSDK는 재생, 버퍼링 및 장치에 대한 자세한 통계를 제공합니다.

TVSDK는 다운로드한 다음 리소스에 대한 정보도 제공합니다.

1. 재생 목록/매니페스트 파일
1. 파일 조각
1. 파일에 대한 추적 정보

   조각과 트랙 같은 다운로드한 리소스에 대한 QoS(서비스 품질) 정보를 `LoadInfo` 클래스.

1. 구현 `onLoadInfo` 콜백 이벤트 리스너입니다.
1. 조각이 다운로드될 때마다 TVSDK가 호출하는 이벤트 리스너를 등록합니다.
1. 에서 관심 데이터 읽기 `LoadInfo` 콜백에 전달되는 매개 변수입니다.

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
    <thead> 
      <tr> 
      <th colname="col01" class="entry"> 속성 </th> 
      <th colname="col1" class="entry"> 유형 </th> 
      <th colname="col2" class="entry"> 설명 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> 길게 </span> </td> 
      <td colname="col2"> <p>다운로드 기간(밀리초)입니다. </p> <p>TVSDK는 클라이언트가 서버에 연결하는 데 걸린 시간과 전체 조각을 다운로드하는 데 걸린 시간을 구분하지 않습니다. 예를 들어 10MB 세그먼트가 다운로드하는 데 8초가 걸리는 경우 TVSDK는 해당 정보를 제공하지만, 첫 번째 바이트까지 4초가 걸리고 전체 조각을 다운로드하는 데 4초가 걸렸다는 정보는 제공하지 않습니다. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> 길게 </span> </td> 
      <td colname="col2"> 다운로드한 조각의 미디어 기간(밀리초)입니다. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> 다운로드한 리소스와 연결된 타임라인 기간 인덱스입니다. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 크기 </span> </td> 
      <td colname="col1"> <span class="codeph"> 길게 </span> </td> 
      <td colname="col2"> 다운로드한 리소스의 크기(바이트)입니다. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> 해당 트랙의 인덱스입니다(알고 있는 경우). 그렇지 않은 경우 0입니다. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <span class="codeph"> 문자열 </span> </td> 
      <td colname="col2"> 해당 트랙의 이름(알려진 경우). 그렇지 않은 경우 null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <span class="codeph"> 문자열 </span> </td> 
      <td colname="col2"> 해당 트랙의 유형(알고 있는 경우). 그렇지 않은 경우 null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 유형 </span> </td> 
      <td colname="col1"> <span class="codeph"> 문자열 </span> </td> 
      <td colname="col2"> TVSDK에서 다운로드한 내용입니다. 다음 중 하나: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST - 재생 목록/매니페스트 </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">조각 - 조각 </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK - 특정 트랙과 연결된 조각 </li> 
      </ul> 리소스 유형을 감지하지 못할 수도 있습니다. 이 경우 FILE이 반환됩니다. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> 문자열 </span> </td> 
      <td colname="col2"> 다운로드한 리소스를 가리키는 URL입니다. </td> 
      </tr> 
    </tbody> 
   </table>
