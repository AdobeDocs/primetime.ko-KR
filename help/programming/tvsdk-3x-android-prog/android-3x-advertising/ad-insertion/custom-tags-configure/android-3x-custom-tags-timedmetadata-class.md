---
description: TVSDK가 재생 목록/매니페스트에서 구독 중인 태그를 감지하면 플레이어는 자동으로 태그를 처리하고 TimedMetadata 개체의 형태로 표시합니다.
seo-description: TVSDK가 재생 목록/매니페스트에서 구독 중인 태그를 감지하면 플레이어는 자동으로 태그를 처리하고 TimedMetadata 개체의 형태로 표시합니다.
seo-title: Timed metadata class
title: Timed metadata class
uuid: c7b1c1d7-48b3-43c7-aa21-f800d894976d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Timed metadata class {#timed-metadata-class}

TVSDK가 재생 목록/매니페스트에서 구독 중인 태그를 감지하면 플레이어는 자동으로 태그를 처리하고 TimedMetadata 개체의 형태로 표시합니다.

이 클래스는 다음과 같은 요소를 제공합니다.

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b> 속성 </b></th> 
   <th colname="col02" class="entry"> <b> 유형 </b></th> 
   <th colname="col2" class="entry"> <b> 설명 </b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>시간 지정 메타데이터의 고유 식별자입니다. </p> <p>이 값은 일반적으로 cue/tag ID 속성에서 추출됩니다. 그렇지 않으면 고유한 임의 값이 제공됩니다. get <span class="codeph"> Id를 </span>사용합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 메타데이터 </span> </td> 
   <td colname="col02"> 메타데이터 </td> 
   <td colname="col2"> <p>재생 목록/매니페스트 사용자 지정 태그에서 처리/압축을 푼 정보입니다. 메타데이터 <span class="codeph"> 가져오기를 </span>사용합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> 문자열 </td> 
   <td colname="col2"> <p>시간 지정 메타데이터의 이름입니다. 유형이 TAG인 <span class="codeph"> 경우 </span>이 값은 cue/tag 이름을 나타냅니다. 유형이 ID <span class="codeph"> 3인 </span>경우 null입니다. get <span class="codeph"> Name을 </span>사용합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> time </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>이 시간 메타데이터가 스트림에 있는 기본 컨텐츠의 시작을 기준으로 시간 위치(밀리초)입니다. get <span class="codeph"> Time을 </span>사용합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> 유형 </td> 
   <td colname="col2"> <p>시간 지정 메타데이터의 유형입니다. get <span class="codeph"> Type을 </span>사용합니다. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - 재생 목록/매니페스트의 태그에서 시간 메타데이터를 만들었음을 나타냅니다. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - 시간 지정 메타데이터가 미디어 스트림의 ID3 태그에서 작성되었음을 나타냅니다. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

다음 사항을 기억하십시오.

* TVSDK는 속성 목록을 키-값 쌍으로 자동으로 추출하고 해당 속성을 메타데이터 속성에 저장합니다.

   >[!TIP]
   >
   >매니페스트의 사용자 지정 태그의 복잡한 데이터(예: 특수 문자가 있는 문자열)는 따옴표로 묶어야 합니다. 예:  >
   >
   >
   ```>
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```  >
   >



* 사용자 지정 태그 형식으로 인해 추출이 실패하는 경우 메타데이터 속성이 비어 있고 응용 프로그램에서 실제 정보를 추출해야 합니다. 이 경우 오류가 발생하지 않습니다.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>요소 </b></th> 
   <th colname="col2" class="entry"> <b>설명</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 공개 열거형 유형 {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>시간 메타데이터에 사용할 수 있는 유형입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(유형 유형, 긴 시간, 긴 id, 문자열 이름, 메타데이터); </span> </td> 
   <td colname="col2"> <p>기본 생성자(시간은 로컬 스트림 시간). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>이 메타데이터가 스트림에 삽입된 기본 컨텐츠의 시작을 기준으로 한 시간 위치입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Metadata getMetadata(); </span> </td> 
   <td colname="col2"> <p>스트림에 삽입된 메타데이터입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>시간 지정 메타데이터의 유형을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>cue/tag 속성에서 추출한 ID를 반환합니다. 그렇지 않으면 고유한 임의 값이 제공됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName(); </span> </td> 
   <td colname="col2"> <p>일반적으로 HLS 태그 이름인 큐의 이름을 반환합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>