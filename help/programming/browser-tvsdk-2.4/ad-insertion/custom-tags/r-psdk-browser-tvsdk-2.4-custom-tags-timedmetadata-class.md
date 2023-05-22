---
description: 브라우저 TVSDK가 재생 목록/매니페스트에서 구독한 태그를 검색하면 플레이어가 자동으로 태그를 처리하여 TimedMetadata 개체로 노출합니다.
title: 시간 메타데이터 클래스
exl-id: 893879b5-03ed-4c11-80a6-b57b7d54a95c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 시간 메타데이터 클래스{#timed-metadata-class}

브라우저 TVSDK가 재생 목록/매니페스트에서 구독한 태그를 검색하면 플레이어가 자동으로 태그를 처리하여 TimedMetadata 개체로 노출합니다.

다음 `TimedMetadata` class는 다음 요소를 제공합니다.

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 속성 </th> 
   <th colname="col02" class="entry"> 유형 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>유형 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetaType</span> </p> </td> 
   <td colname="col2"> <p>다음은 시간 메타데이터 유형입니다. 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">태그 - 재생 목록/매니페스트의 태그에서 시간 메타데이터가 생성되었습니다. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 - 미디어 스트림의 ID3 태그에서 시간 메타데이터가 생성되었습니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>시간 </p> </td> 
   <td colname="col02"> <p>숫자 </p> </td> 
   <td colname="col2"> <p>이 시간 메타데이터가 스트림에 있는 기본 콘텐츠의 시작과 상대적인 로컬 시간 위치(밀리초)입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>문자열 </p> </td> 
   <td colname="col2"> <p>시간 메타데이터의 고유 식별자입니다. </p> <p>는 일반적으로 존재하는 경우 큐/태그 ID 속성에서 추출됩니다. 그렇지 않으면 고유한 임의 값입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>이름 </p> </td> 
   <td colname="col02"> <p>숫자 </p> </td> 
   <td colname="col2"> <p>시간 메타데이터의 이름입니다. </p> <p>유형이 TAG이면 값은 큐/태그 이름을 나타냅니다. 유형이 ID3이면 값은 null입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>콘텐츠 </p> </td> 
   <td colname="col02"> <p>문자열 </p> </td> 
   <td colname="col2"> <p>시간 메타데이터의 원시 콘텐츠입니다. </p> <p>유형이 TAG이면 값은 큐/태그의 전체 속성 목록을 나타냅니다. 유형 ID3이면 값은 null입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>메타데이터 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> 메타데이터</span> </p> </td> 
   <td colname="col2"> <p>재생 목록/매니페스트 사용자 지정 태그에서 처리/추출된 정보. </p> </td> 
  </tr> 
 </tbody> 
</table>
