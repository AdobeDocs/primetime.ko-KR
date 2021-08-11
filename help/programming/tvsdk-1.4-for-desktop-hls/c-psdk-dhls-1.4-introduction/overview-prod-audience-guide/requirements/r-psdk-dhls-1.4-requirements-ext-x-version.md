---
description: .m3u8 파일의 EXT-X-VERSION 버전은 응용 프로그램에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 유효한 EXT 태그에 영향을 줍니다.
title: EXT-X 버전 요구 사항
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# EXT-X 버전 요구 사항{#ext-x-version-requirements}

.m3u8 파일의 #EXT-X-VERSION 버전은 응용 프로그램에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 유효한 EXT 태그에 영향을 줍니다.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

다음은 HLS 프로토콜 버전을 지정하는 `#EXT-X-VERSION` 태그에 대한 정보입니다.

* 버전은 HLS 재생 목록의 기능과 속성과 일치해야 합니다. 그렇지 않으면 재생 오류가 발생할 수 있습니다.

   자세한 내용은 [HTTP 라이브 스트리밍 사양](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)을 참조하십시오.
* 버전은 HLS 재생 목록의 기능과 속성과 일치해야 합니다. 그렇지 않으면 재생 오류가 발생할 수 있습니다.

   자세한 내용은 [HTTP 라이브 스트리밍 사양](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)을 참조하십시오.
* Adobe은 기반 클라이언트에서 재생하는 데 버전 2 이상을 사용하는 것이 좋습니다.

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span> 태그의 IV 속성입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">부동 소수점 <span class="codeph"> EXTINF </span> 기간 값 <p>기간 태그( <span class="codeph"> #EXTINF: 버전 2의 </span>&lt;duration&gt;,&lt;title&gt;)가 정수 값으로 반올림되었습니다. 버전 3 이상에서는 부동 소수점에서 지속 시간을 정확히 지정해야 합니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6"><span class="codeph"> EXT-X-BYTERANGE </span> 태그 </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> 태그 </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD"><span class="codeph"> EXT-X-I-FRAMES-ONLY </span> 태그 </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB"><span class="codeph"> EXT-X-MEDIA </span> 태그 </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C"><span class="codeph"> EXT-X-STREAM-INF </span> 태그의 <span class="codeph"> AUDIO </span> 및 <span class="codeph"> VIDEO </span> 속성 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK 대체 오디오 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
