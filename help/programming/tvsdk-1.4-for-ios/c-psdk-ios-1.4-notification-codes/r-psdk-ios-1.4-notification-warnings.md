---
description: 이 표에서는 WARN 유형 알림에 대한 자세한 정보를 보여 줍니다.
title: 경고 알림 코드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 4%

---


# 경고 알림 코드{#warning-notification-codes}

이 표에서는 WARN 유형 알림에 대한 자세한 정보를 보여 줍니다.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

대부분의 경고에는 다운로드하지 못한 리소스의 URL과 같이 관련 메타데이터가 포함되어 있습니다. 일부 알림에는 주 비디오 컨텐츠, 대체 오디오 컨텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함되어 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 코드 </th> 
   <th colname="2" class="entry"> 이름 </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> 메타데이터 키 </th> 
   <th colname="5" class="entry"> 댓글 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>광고 해결</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002년</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>광고 크리에이티브를 로드하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003년</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR, AD_ID,DESCRIPTION</span> </td> 
   <td colname="5"> <p>잘못된 VAST URL 또는 VAST 래퍼에서 반환된 광고가 없어 광고 해결에 실패했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>배경 매니페스트</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000  </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_경고</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> ERRORBACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> NAME 설명</span> </td> 
   <td colname="5"> <p> 백그라운드 매니페스트 다운로드에 오류가 있습니다. 배경 매니페스트를 업데이트할 때 TV SDK 경고로 전달되고 재생이 중지되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001년  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_WARNING</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> <p></p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000  </span> </td> 
   <td colname="2"><span class="codeph"> UNDEFINED_TIME_RANGES  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> 광고 신호 모드는 사용자 지정 범위로 정의되지만 정의된 범위가 없습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001  </span> </td> 
   <td colname="2"><span class="codeph"> 잘못된_TIME_범위  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> <p> 하나 이상의 시간 범위가 잘못되어 무시되거나 수정됩니다. </p> <p> DESCRIPTION은 잘못된 범위에 대한 설명을 포함하는 문자열입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS 관련</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_NOT_READY  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>AD가 스트림에 삽입되지 않았습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002  </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING  </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>광고에 오디오 전용 스트림이 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING  </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>컨텐츠의 현재 비트 전송률에 대해 일치하는 광고 스트림을 찾을 수 없습니다. </p> <p>  </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270005  </span> </td> 
   <td colname="2"><span class="codeph"> AVASSET_FAILED_TO_CREATE  </span> </td> 
   <td colname="3"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>AVAsset을 만드는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270006  </span> </td> 
   <td colname="2"><span class="codeph"> SiteCatalyst_경고  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> <p>경고:sitecatalyst 경고 설명을 참조하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270007  </span> </td> 
   <td colname="2"><span class="codeph"> NETWORK_ERROR  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> <p>네트워크에서 데이터를 가져오는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002</span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>이 광고에 대한 오디오가 누락되어 들을 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003</span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>일치하는 비트 전송률이 없습니다. </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID 및 소스(URL)는 `AD_ASSET` 키를 사용하여 알림 메타데이터의 PTAdAsset를 통해 검색할 수 있습니다.
