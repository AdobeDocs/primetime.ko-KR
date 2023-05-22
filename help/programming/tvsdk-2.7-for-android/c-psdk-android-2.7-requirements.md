---
description: TVSDK에는 미디어 콘텐츠, 매니페스트 콘텐츠, DRM 및 소프트웨어 버전에 대한 특정 요구 사항이 있습니다.
title: 요구 사항
exl-id: 8c252761-eee3-4fec-a85f-a38c1d9be9cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 요구 사항 {#requirements}

TVSDK에는 미디어 콘텐츠, 매니페스트 콘텐츠, DRM 및 소프트웨어 버전에 대한 특정 요구 사항이 있습니다.

## 시스템 및 소프트웨어 요구 사항 {#section_96E5B079900246E78682AE44D3F23068}

TVSDK를 사용하려면 하드웨어, 운영 체제 및 애플리케이션 버전이 모두 아래에 나열된 최소 요구 사항을 충족하는지 확인하십시오.

| 운영 체제 | Android 4.0 이상(최소 API 레벨 14) |
|---|---|
| CPU | 1GHz 싱글 코어 또는 동급 코어 |
| RAM | 256 MB |
| GPU | 재생에 필요한 하드웨어 GPU |
| 아키텍처 | Houdini, ARM64, ARMv7 및 ARMv8을 통한 x86 |

## 컨텐츠 및 매니페스트 요구 사항 {#section_72DD0E4DA9774DCCADB42887497F1386}

DRM 암호화 키를 포함하여 스트림 및 재생 목록(매니페스트)에 대한 제한 및 요구 사항을 확인하십시오.

| Adobe 액세스 DRM | DRM 보호 스트림이 MBR(Multiple Bit Rate)인 경우, MBR에 사용되는 DRM 암호화 키는 모든 비트 레이트 스트림에서 사용되는 키와 동일해야 한다. |
|---|---|
| 광고 변형 매니페스트 | 기본 콘텐츠 렌디션과 동일한 비트율 렌디션을 가져야 합니다. |

## #EXT-X-VERSION 요구 사항 {#section_49A33664651A46EC9ED888BA9C1C3F6D}

[!DNL .m3u8] 매니페스트 파일의 `#EXT-X-VERSION` 버전은 응용 프로그램에서 사용할 수 있는 기능과 올바른 `EXT` 태그에 영향을 줍니다.

다음은 HLS 프로토콜 버전을 지정하는 `#EXT-X-VERSION` 태그에 대한 정보입니다.

* 버전은 HLS 재생 목록의 기능 및 속성과 일치해야 합니다. 그렇지 않으면 재생 오류가 발생할 수 있습니다. 자세한 내용은 [HTTP 라이브 스트리밍 사양](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe은 TVSDK 기반 클라이언트에서 재생하기 위해 HLS 버전 2 이상을 사용할 것을 권장합니다.

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> 의 IV 속성 <span class="codeph"> X-키 </span> 태그에 가깝게 배치하십시오. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">부동 소수점 <span class="codeph"> EXTINA </span> 기간 값 <p>버전 2의 기간 태그( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;)가 정수 값으로 반올림되었습니다. 버전 3 이상에서는 지속 시간을 부동 소수점에 정확히 지정해야 합니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">다음 <span class="codeph"> EXT-X-BYTERANGE </span> 태그 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">다음 <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> 태그 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">다음 <span class="codeph"> EXT-X-I-FRAMES 전용 </span> 태그 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">다음 <span class="codeph"> EXT-X-MEDIA </span> 태그 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">다음 <span class="codeph"> 오디오 </span> 및 <span class="codeph"> 비디오 </span> 의 속성 <span class="codeph"> EXT-X-STREAM-INF </span> 태그 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK 대체 오디오 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
