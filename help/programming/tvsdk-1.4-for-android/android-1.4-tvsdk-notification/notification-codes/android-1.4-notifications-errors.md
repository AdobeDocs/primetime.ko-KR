---
description: 이 표에서는 ERROR 유형 알림에 대한 자세한 정보를 제공합니다.
title: 오류 알림 코드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 4%

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
   <td colname="1"><b>재생</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> 조각 또는 세그먼트(비디오 및 오디오 모두)를 다운로드하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008년  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> DESIRED_SEEK_POSITION  </span><span class="codeph"> DESIRED_SEEK_PERIOD  </span> </td> 
   <td colname="5"> 검색 작업을 수행하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009년  </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> 일시 정지 작업을 수행하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102  </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> 컨텐츠 기간에 대한 정보를 검색하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103  </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> 재생 위치를 검색하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104  </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> QOS 정보를 검색하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200  </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> 데이터 다운로드를 시도하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>잘못된 리소스</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span><span class="codeph"> 리소스  </span> </td> 
   <td colname="5"> 리소스 항목을 로드하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_FAILED  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span> </td> 
   <td colname="5"> 재생 타임라인에 리소스를 배치하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>광고 처리</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID  </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL  </span><span class="codeph"> AD_RESOLVE_FAIL  </span><span class="codeph"> AD_RESOLVER_SERVER_UNACABLE  </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> 없음 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> 잘못된 광고 메타데이터 형식으로 인해 광고 해결에 실패했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_ 실패  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
   <td colname="5"> 광고 플러그인이 광고를 확인하지 못했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> PROPOSED_AD_BREAK</span> </td> 
   <td colname="5"> 광고 단계를 확인하지 못했습니다. </td> 
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
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_CODE  </span> <span class="codeph"> NATIVE_ERROR_NAME  </span> <span class="codeph"> 설명  </span> <span class="codeph"> 설명</span> <p><b>DRM 세부 정보:</b> </p> <span class="codeph"> DRM_ERROR_</span> <span class="codeph"> STRINGNATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>하위 수준 AVE 라이브러리에서 오류가 발생했습니다. </p> <p>이러한 메타데이터 키 값에 대한 자세한 내용은 <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR 알림</a>에 대한 세부 정보를 참조하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> AVE 하위 수준 라이브러리를 인스턴스화하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> AVE 하위 수준 라이브러리를 해제하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> AVE 라이브러리에서 사용하는 GPU 리소스를 해제하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> AVE 라이브러리를 재설정하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> AVE 라이브러리에 보기를 연결하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>구성</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107000  </span> </td> 
   <td colname="2"><span class="codeph"> SET_VOLUME_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명 볼륨  </span> </td> 
   <td colname="5"> 볼륨 수준을 설정하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107001  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_ 오류  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> 버퍼링 매개 변수를 변경하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> CC 트랙의 가시성을 변경하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> CC 트랙의 스타일 옵션을 변경하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107004  </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_ 오류  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> ABR 컨트롤 매개 변수를 변경하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107005  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명  </span><span class="codeph"> INITIAL_BUFFER_TIME  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> 버퍼링 컨트롤 매개 변수를 변경하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>대체 오디오</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR  </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME  </span><span class="codeph"> AUDIO_TRACK_LANGUAGE  </span> </td> 
   <td colname="5"> 오디오 트랙과 관련된 오류가 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>일반</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 19999년  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR</span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> 일반 오류 이벤트를 표시합니다. 실제로 TVSDK에서 발행되지 않습니다. 이것은 TVSDK 오류 이벤트에 해당하는 숫자 코드 범위의 끝에 대한 마커입니다. </td> 
  </tr> 
 </tbody> 
</table>

