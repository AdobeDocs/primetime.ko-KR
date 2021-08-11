---
description: .m3u8 파일의 '#'EXT-X-VERSION 버전은 응용 프로그램에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 유효한 EXT 태그에 영향을 줍니다.
title: '''#''EXT-X-VERSION 요구 사항'
exl-id: 1b7c205b-c6b1-416f-885a-d1cd23d8e803
source-git-commit: 8610792a7410dab59d42ab7771b534c2c1670ad2
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `#`EXT-X 버전 요구 사항{#ext-x-version-requirements}

.m3u8 파일의 #EXT-X-VERSION 버전은 응용 프로그램에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 유효한 EXT 태그에 영향을 줍니다.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

다음은 HLS 프로토콜 버전을 지정하는 `#EXT-X-VERSION` 태그에 대한 정보입니다.

* 버전은 HLS 재생 목록의 기능과 속성과 일치해야 합니다. 그렇지 않으면 재생 오류가 발생할 수 있습니다. 자세한 내용은 [HTTP 라이브 스트리밍 사양](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)을 참조하십시오.
* Adobe은 브라우저 TVSDK 기반 클라이언트에서 재생하기 위해 버전 2 이상을 사용할 것을 권장합니다.

   클라이언트와 서버는 다음 방법으로 버전을 구현해야 합니다.

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이 버전 이상 사용 </th> 
   <th colname="2" class="entry"> 이러한 기능을 사용하려면 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">부동 소수점 <span class="codeph"> EXTINF </span> 기간 값 <p>기간 태그( <span class="codeph"> #EXTINF: 버전 2의 </span>&lt;duration&gt;,&lt;title&gt;)가 정수 값으로 반올림되었습니다. 버전 3 이상에서는 부동 소수점에서 지속 시간을 정확히 지정해야 합니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B"><span class="codeph"> EXT-X-MEDIA </span> 태그 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD"><span class="codeph"> EXT-X-STREAM-INF </span> 태그의 <span class="codeph"> AUDIO </span> 및 <span class="codeph"> VIDEO </span> 속성 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
