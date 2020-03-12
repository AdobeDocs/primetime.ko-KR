---
description: '.m3u8 파일의 #EXT-X-VERSION 버전은 애플리케이션에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 사용할 수 있는 EXT 태그에 영향을 줍니다.'
seo-description: '.m3u8 파일의 #EXT-X-VERSION 버전은 애플리케이션에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 사용할 수 있는 EXT 태그에 영향을 줍니다.'
seo-title: '#EXT-X-VERSION 요구 사항'
title: '#EXT-X-VERSION 요구 사항'
uuid: c862df4a-88ba-4497-8b7c-b83fcb34b8bb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# #EXT-X-VERSION 요구 사항{#ext-x-version-requirements}

.m3u8 파일의 #EXT-X-VERSION 버전은 애플리케이션에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 사용할 수 있는 EXT 태그에 영향을 줍니다.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

다음은 HLS 프로토콜 버전을 지정하는 `#EXT-X-VERSION` 태그에 대한 정보입니다.

* 버전은 HLS 재생 목록의 기능과 속성과 일치해야 합니다.그렇지 않으면 재생 오류가 발생할 수 있습니다.

   자세한 내용은 HTTP Live [스트리밍 사양을](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)참조하십시오.
* 버전은 HLS 재생 목록의 기능과 속성과 일치해야 합니다.그렇지 않으면 재생 오류가 발생할 수 있습니다.

   자세한 내용은 HTTP Live [스트리밍 사양을](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)참조하십시오.
* Adobe는 최소 버전 2를 사용하여 클라이언트 기반의 재생을 권장합니다.

   클라이언트 및 서버는 다음 방법으로 버전을 구현해야 합니다.

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이 버전 이상 사용 </th> 
   <th colname="2" class="entry"> 이러한 기능을 사용하려면 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> EXT-X-KEY <span class="codeph"></span> 태그의 IV 속성입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">부동 소수점 <span class="codeph"> EXTINF </span> 지속 시간 값 <p>지속 시간 태그( <span class="codeph"> #EXTENINF:버전 2의 </span>&lt;duration&gt;,&lt;title&gt;)이 정수 값으로 반올림되었습니다. 버전 3 이상에서는 부동 소수점에서 기간을 정확히 지정해야 합니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">EXT- <span class="codeph"> X-BYTERANGE </span> 태그 </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">EXT- <span class="codeph"> X-I-FRAME-STREAM-INF </span> 태그 </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">EXT- <span class="codeph"> X-I-FRAMES-ONLY </span> 태그 </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">EXT- <span class="codeph"> X-MEDIA </span> 태그 </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">EXT- <span class="codeph"> X-STREAM-INF </span> <span class="codeph"> 태그의 오디오 및 비디오 </span> <span class="codeph"> </span> 속성 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK 대체 오디오 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

