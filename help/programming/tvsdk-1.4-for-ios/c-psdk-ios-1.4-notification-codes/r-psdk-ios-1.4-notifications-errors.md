---
description: 이 표에서는 ERROR 유형 알림에 대한 자세한 정보를 제공합니다.
title: 오류 알림 코드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 5%

---


# 오류 알림 코드{#error-notification-codes}

이 표에서는 ERROR 유형 알림에 대한 자세한 정보를 제공합니다.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

대부분의 오류에는 관련 메타데이터가 포함됩니다(예: 다운로드하지 못한 리소스의 URL). 일부 알림에는 주 비디오 컨텐츠, 대체 오디오 컨텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함되어 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
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
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000  </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR  </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE  </span><span class="codeph"> MINOR_DRM_CODE  </span><span class="codeph"> 설명  </span> </td> 
   <td colname="5"></td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>재생</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="3"></td> 
   <td colname="4"></td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101001  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span><span class="codeph"> INTERNAL_ERROR  </span><span class="codeph"> URL  </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008년  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> <p>검색 작업을 수행하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009년  </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>일시 정지 작업을 수행하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101101  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY  </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>  </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>잘못된 리소스</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102000  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_MEDIA_PLAYER_ITEM  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>광고 처리</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID  </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED</span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>잘못된 광고 메타데이터 형식으로 인해 광고 해결에 실패했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED  </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>광고 단계를 확인하지 못했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006  </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>기본</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> INTERNAL_ERROR  </span> </td> 
   <td colname="5"> <p>하위 수준 iOS 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>구성</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>CC 트랙의 가시성을 변경하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR  </span> </td> 
   <td colname="3"> <span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>CC 트랙의 스타일 옵션을 변경하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS 고유</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_VERSION_ 호환되지 않음  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>광고의 HLS 버전은 컨텐츠의 HLS 버전보다 높습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170001  </span> </td> 
   <td colname="2"><span class="codeph"> ARGUMENT_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>인수 오류 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170002  </span> </td> 
   <td colname="2"><span class="codeph"> M3U8_PARSER_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> <p>m3u8을 구문 분석할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170003  </span> </td> 
   <td colname="2"><span class="codeph"> WEBVTT_PARSER_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>Webvtt을 구문 분석할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170004  </span> </td> 
   <td colname="2"><span class="codeph"> HLS_SEGMENT_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span><span class="codeph"> URL  </span><span class="codeph"> INTERNAL_ERROR  </span> </td> 
   <td colname="5"> <p>세그먼트가 변형의 지정된 대역폭을 초과합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170005  </span> </td> 
   <td colname="2"><span class="codeph"> MBR_MEDIASEQUENCE_OFFSYNC  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>미디어 시퀀스 번호가 이 MBR의 모든 HLS 스트림에서 동기화되지 않았습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170006  </span> </td> 
   <td colname="2"><span class="codeph"> MISSING_FILE_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span><span class="codeph"> URL  </span><span class="codeph"> INTERNAL_ERROR  </span> </td> 
   <td colname="5"> <p>파일이 없거나 응답하지 않습니다. </p> <p>HTTP 404:파일을 찾을 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170007  </span> </td> 
   <td colname="2"><span class="codeph"> AD_EMPTY_RESPONSE  </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>광고를 검색할 수 없습니다. 빈 응답입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170008  </span> </td> 
   <td colname="2"><span class="codeph"> AD_TIMEOUT  </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>광고를 검색할 수 없습니다. 시간 초과 오류입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170009  </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLE_TRACK_CHANGE_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY  </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>자막 트랙을 변경하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170010  </span> </td> 
   <td colname="2"><span class="codeph"> SiteCatalyst_오류  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> <p>Site catalyst 오류입니다. 설명을 참조하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170011  </span> </td> 
   <td colname="2"><span class="codeph"> AD_TARGET_DURATION_INCOMPATIBLE  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>광고의 TARGET 지속 시간은 컨텐츠의 TARGET 지속 시간보다 높습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID 및 소스(URL)는 `AD_ASSET` 키를 사용하여 알림 메타데이터의 `PTAdAsset`을 통해 검색할 수 있습니다.
