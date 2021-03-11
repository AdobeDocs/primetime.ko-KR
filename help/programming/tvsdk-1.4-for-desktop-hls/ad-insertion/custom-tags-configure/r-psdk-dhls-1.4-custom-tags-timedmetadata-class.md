---
description: TVSDK가 재생 목록/매니페스트에서 구독 태그를 감지하면 플레이어는 자동으로 태그를 처리하고 TimedMetadata 객체의 형태로 표시합니다.
title: Timed metadata 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Timed metadata 클래스{#timed-metadata-class}

TVSDK가 재생 목록/매니페스트에서 구독 태그를 감지하면 플레이어는 자동으로 태그를 처리하고 TimedMetadata 객체의 형태로 표시합니다.

이 클래스는 다음과 같은 요소를 제공합니다.

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 속성 </th> 
   <th colname="col02" class="entry"> 유형 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> 콘텐트</span> </td> 
   <td colname="col02"> 문자열 </td> 
   <td colname="col2"> 시간 지정 메타데이터의 원시 컨텐츠입니다. 유형이 TAG인 경우 이 값은 cue/tag의 전체 속성 목록을 나타냅니다. 유형 ID3의 경우 null입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> id</span> </td> 
   <td colname="col02"> 문자열 </td> 
   <td colname="col2"> 시간 지정 메타데이터의 고유 식별자입니다. 이 값은 일반적으로 큐/태그 ID 속성에서 추출됩니다. 그렇지 않으면 고유한 임의 값이 제공됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 메타데이터</span> </td> 
   <td colname="col02"> 메타데이터 </td> 
   <td colname="col2"> 재생 목록/매니페스트 사용자 지정 태그에서 처리/추출 정보입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"> 문자열 </td> 
   <td colname="col2">시간 지정 메타데이터의 이름입니다. 유형이 <span class="codeph"> TAG</span>인 경우 값은 cue/tag 이름을 나타냅니다. 유형이 <span class="codeph"> ID3</span>이면 null입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> time</span> </td> 
   <td colname="col02"> 숫자 </td> 
   <td colname="col2"> 이 시간 메타데이터가 스트림에 있는 기본 컨텐츠의 시작을 기준으로 하는 시간 위치(밀리초)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> 문자열 </td> 
   <td colname="col2">시간 지정 메타데이터의 유형입니다. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - 재생 목록/매니페스트의 태그에서 시간 메타데이터를 만들었음을 나타냅니다. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - 미디어 스트림의 ID3 태그에서 시간 지정 메타데이터를 만들었음을 나타냅니다. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

다음 사항을 기억하십시오.

* TVSDK는 속성 목록을 키-값 쌍으로 자동으로 추출하고 해당 속성을 메타데이터 속성에 저장합니다.

   >[!TIP]
   >
   >특수 문자가 있는 문자열 등 매니페스트의 사용자 지정 태그의 복잡한 데이터는 따옴표로 묶어야 합니다. 예:
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* 사용자 지정 태그 형식으로 인해 추출에 실패하는 경우 메타데이터 속성은 비어 있고 응용 프로그램은 실제 정보를 추출해야 합니다. 이 경우 오류가 발생하지 않습니다.

| 요소 | 설명 |
|---|---|
| `TAG, ID3 ID3, TAG` | 시간 지정 메타데이터에 대해 가능한 유형입니다. |
| `public function TimedMetadata(type:String, time:Number, id:String, name:String, content:String, metadata:Metadata)` | 기본 생성자(시간은 로컬 스트림 시간입니다). |
| `content:String` | 이 시간 지정 메타데이터의 소스 태그의 원시 컨텐츠입니다. |
| `time:Number` | 이 메타데이터가 스트림에 삽입된 기본 컨텐츠의 시작을 기준으로 하는 시간 위치입니다. |
| `metadata:Metadata` | 스트림에 삽입된 메타데이터입니다. |
| `type:String` | 시간 지정 메타데이터의 유형을 반환합니다. |
| `id:String` | 큐/태그 속성에서 추출된 ID를 반환합니다. 그렇지 않으면 고유한 임의 값이 제공됩니다. |
| `name:String` | 일반적으로 HLS 태그 이름인 큐 이름을 반환합니다. |

