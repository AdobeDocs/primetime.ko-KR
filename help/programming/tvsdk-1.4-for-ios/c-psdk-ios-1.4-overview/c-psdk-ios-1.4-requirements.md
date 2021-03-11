---
description: TVSDK에는 미디어 컨텐츠, 매니페스트 컨텐츠 및 소프트웨어 버전에 대한 특정 속성이 필요합니다.
title: 요구 사항
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 요구 사항 {#requirements}

TVSDK에는 미디어 컨텐츠, 매니페스트 컨텐츠 및 소프트웨어 버전에 대한 특정 속성이 필요합니다.

## 시스템 및 소프트웨어 요구 사항 {#section_61C32A0209C44230B392B113B85643EE}

TVSDK를 사용하려면 하드웨어, 운영 체제 및 애플리케이션 버전이 모두 아래 나열된 최소 요구 사항을 충족하는지 확인하십시오.

운영 체제:iOS 6.0 이상

## 콘텐트 및 매니페스트 요구 사항 {#section_05FA02E2189742008DA09D87E66DCAB7}

DRM 암호화 키를 비롯한 스트림 및 재생 목록(매니페스트)에 대한 제한 사항 및 요구 사항을 확인합니다.

| 컨텐츠 세그먼트 키 프레임 | 각 컨텐츠 세그먼트는 키 프레임으로 시작해야 합니다. |
|---|---|
| 라이브/선형 비디오의 시퀀스 번호 | 기본 컨텐츠에 대한 모든 비트 전송률 변환은 지정된 시간에 일치해야 합니다. |

## #EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

[!DNL .m3u8] 파일의 `#EXT-X-VERSION` 버전은 응용 프로그램에서 사용할 수 있는 기능과 재생 목록/매니페스트에서 사용할 수 있는 `EXT` 태그에 영향을 줍니다.

다음은 HLS 프로토콜 버전을 지정하는 `#EXT-X-VERSION` 태그에 대한 몇 가지 정보입니다.

* 버전은 HLS 재생 목록의 기능과 속성과 일치해야 합니다.그렇지 않으면 재생 오류가 발생할 수 있습니다.

   자세한 내용은 [HTTP 라이브 스트리밍 사양](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)을 참조하십시오.
* 태그가 마스터 또는 미디어 재생 목록에 포함되어 있지 않거나 버전이 지정되지 않은 경우 버전 1이 기본적으로 사용됩니다. 버전 1을 준수하지 않는 컨텐츠는 재생되지 않습니다.
* Adobe은 TVSDK 기반 클라이언트에서 재생하려면 버전 2 이상을 사용하는 것이 좋습니다.

클라이언트 및 서버는 다음 방법으로 버전을 구현해야 합니다.

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> 적어도 이 버전 사용 </th> 
   <th colname="2" class="entry"> 이러한 기능을 사용하려면 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span> 태그의 IV 속성입니다. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">부동 소수점 <span class="codeph"> EXTENINF </span> 지속 시간 값 <p>기간 태그( <span class="codeph"> #EXTINF:버전 2의 </span>&lt;duration&gt;,&lt;title&gt;)이 정수 값으로 반올림되었습니다. 버전 3 이상을 사용하려면 부동 소수점 형식의 지속 시간이 필요합니다. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> 광고 삽입 및 완벽한 ABR과 같은 TVSDK 기능 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927"><span class="codeph"> EXT-X-BYTERANGE </span> 태그 </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> 태그 </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10"><span class="codeph"> EXT-X-I-FRAMES-ONLY </span> 태그 </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2"><span class="codeph"> EXT-X-MEDIA </span> 태그 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34"><span class="codeph"> EXT-X-STREAM-INF </span> 태그의 <span class="codeph"> AUDIO </span> 및 <span class="codeph"> VIDEO </span> 속성 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK 대체 오디오 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
