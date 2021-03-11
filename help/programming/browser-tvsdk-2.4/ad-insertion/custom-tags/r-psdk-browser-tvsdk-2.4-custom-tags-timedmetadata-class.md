---
description: Browser TVSDK가 재생 목록/매니페스트에서 구독 태그를 감지하면 플레이어는 자동으로 태그를 처리하고 TimedMetadata 객체로 표시합니다.
title: Timed metadata 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Timed metadata 클래스{#timed-metadata-class}

Browser TVSDK가 재생 목록/매니페스트에서 구독 태그를 감지하면 플레이어는 자동으로 태그를 처리하고 TimedMetadata 객체로 표시합니다.

`TimedMetadata` 클래스는 다음 요소를 제공합니다.

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
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>다음은 시간 지정 메타데이터 유형입니다. 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG - 재생 목록/매니페스트의 태그에서 시간 메타데이터를 만들었습니다. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 - 미디어 스트림의 ID3 태그에서 시간 지정 메타데이터를 만들었습니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>time </p> </td> 
   <td colname="col02"> <p>숫자 </p> </td> 
   <td colname="col2"> <p>이 시간 지정 메타데이터가 스트림에 있는 기본 컨텐츠의 시작을 기준으로 하는 로컬 시간 위치(밀리초)입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>문자열 </p> </td> 
   <td colname="col2"> <p>시간 지정 메타데이터의 고유 식별자입니다. </p> <p>은 대개 큐/태그 ID 속성이 있는 경우 추출됩니다. 그렇지 않으면 고유한 임의 값입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>숫자 </p> </td> 
   <td colname="col2"> <p>시간 지정 메타데이터의 이름입니다. </p> <p>유형이 TAG인 경우 값은 cue/tag 이름을 나타냅니다. 유형이 ID3이면 값은 null입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>콘텐트 </p> </td> 
   <td colname="col02"> <p>문자열 </p> </td> 
   <td colname="col2"> <p>시간 지정 메타데이터의 원시 컨텐츠입니다. </p> <p>유형이 TAG인 경우 이 값은 cue/tag의 전체 속성 목록을 나타냅니다. 유형 ID3의 경우 이 값은 null입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>메타데이터 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> 메타데이터</span> </p> </td> 
   <td colname="col2"> <p>재생 목록/매니페스트 사용자 지정 태그에서 처리/추출 정보입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

