---
description: TVSDK가 재생 목록/매니페스트에서 구독한 태그를 검색하면 플레이어가 자동으로 태그를 처리하여 PTTimedMetadata 개체의 형태로 노출합니다.
title: 시간 메타데이터 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 시간 메타데이터 클래스{#timed-metadata-class}

TVSDK가 재생 목록/매니페스트에서 구독한 태그를 검색하면 플레이어가 자동으로 태그를 처리하여 PTTimedMetadata 개체의 형태로 노출합니다.

클래스는 다음 요소를 제공합니다.

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
   <td colname="col1"> <span class="codeph"> 메타데이터 ID</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> 시간 메타데이터의 고유 식별자입니다. 이 값은 일반적으로 큐/태그 ID 속성에서 추출됩니다. 그렇지 않으면 고유한 임의 값이 제공됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 이름</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> 시간 메타데이터의 이름입니다. 유형이 인 경우 <span class="codeph"> 태그</span>, 값은 큐/태그 이름을 나타냅니다. 유형이 인 경우 <span class="codeph"> ID3</span>, null입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 시간</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> 이 시간 메타데이터가 스트림에 있는 기본 콘텐츠의 시작을 기준으로 한 시간 위치(밀리초)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 유형</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
   <td colname="col2">시간 메타데이터의 유형입니다. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">태그 - 재생 목록/매니페스트의 태그에서 시간 메타데이터가 생성되었음을 나타냅니다. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - 미디어 스트림의 ID3 태그에서 시간 메타데이터가 생성되었음을 나타냅니다. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

다음 사항을 기억하십시오.

* TVSDK는 특성 목록을 키-값 쌍으로 자동으로 추출하고 특성을 메타데이터 속성에 저장합니다.

  >[!TIP]
  >
  >매니페스트의 사용자 지정 태그에 있는 복잡한 데이터(예: 특수 문자가 있는 문자열)는 따옴표로 묶어야 합니다. 예:
  >
  >```
  >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
  >"www.example.com:8090?parameter1=xyz&parameter2=abc"
  >```
  >

* 사용자 지정 태그 형식으로 인해 추출에 실패하는 경우 컨텐츠 속성에는 항상 태그의 원시 데이터(콜론 다음의 문자열)가 포함됩니다. 이 경우 오류가 발생하지 않습니다.

| 요소 | 설명 |
|---|---|
| 태그, ID3 | 시간 메타데이터에 가능한 유형입니다. |
| `@property (nonatomic, assign) CMTime time` | 주 콘텐츠의 시작과 관련하여 이 메타데이터가 스트림에 삽입된 시간 위치입니다. |
| `@property (nonatomic, assign) PTTimedMetadataType type` | 시간 메타데이터의 유형을 반환합니다. |
| `@property (nonatomic, retain) NSString *metadataId` | 큐/태그 특성에서 추출한 ID를 반환합니다. 그렇지 않으면 고유한 임의 값이 제공됩니다. |
| `@property (nonatomic, retain) NSString *name` | 큐의 이름을 반환합니다(일반적으로 HLS 태그 이름). |
