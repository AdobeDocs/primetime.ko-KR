---
description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-title: 'null'
title: 'null'
uuid: 20828188-817a-471c-acbc-aeb5f336356b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 오류 알림 코드 {#error-notification-codes}

이 표에서는 ERROR 유형 알림에 대한 자세한 정보를 제공합니다.

대부분의 오류에는 다운로드하지 못한 리소스의 URL과 같은 관련 메타데이터가 포함되어 있습니다. 일부 알림에는 주 비디오 컨텐츠, 대체 오디오 컨텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함되어 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>코드</b></th> 
   <th colname="2" class="entry"><b>이름</b></th> 
   <th colname="3" class="entry"><b>InnerNotification</b></th> 
   <th colname="4" class="entry"><b>메타데이터 키</b></th> 
   <th colname="5" class="entry"><b>댓글</b></th> 
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
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE </span><span class="codeph"> MINOR_DRM_CODE </span><span class="codeph"> 설명 </span> </td> 
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
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"></td> 
   <td colname="4"></td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101001 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_PLAYBACK_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명 </span><span class="codeph"> INTERNAL_ERROR </span><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> <p>검색 작업을 수행하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>일시 중지 작업을 수행하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101101 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
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
   <td colname="1"><span class="codeph"> 102000 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_MEDIA_PLAYER_ITEM </span> </td> 
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
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED</span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>잘못된 광고 메타데이터 형식으로 인해 광고 해결에 실패했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>광고 해결 단계가 실패했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
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
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> INTERNAL_ERROR </span> </td> 
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
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>CC 트랙의 가시성을 변경하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR </span> </td> 
   <td colname="3"> <span class="codeph"> NATIVE_ERROR </span> </td> 
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
   <td colname="1"><span class="codeph"> 170000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_VERSION_호환되지 않음 </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>광고의 HLS 버전은 컨텐츠의 HLS 버전보다 높습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170001 </span> </td> 
   <td colname="2"><span class="codeph"> ARGUMENT_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>인수 오류 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170002 </span> </td> 
   <td colname="2"><span class="codeph"> M3U8_PARSER_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명 </span> </td> 
   <td colname="5"> <p>m3u8을 구문 분석할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170003 </span> </td> 
   <td colname="2"><span class="codeph"> WEBVTT_PARSER_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>Webvtt을 구문 분석할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170004 </span> </td> 
   <td colname="2"><span class="codeph"> HLS_SEGMENT_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명 </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>세그먼트가 변형의 지정된 대역폭을 초과했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170005 </span> </td> 
   <td colname="2"><span class="codeph"> MBR_MEDIASEQUENCE_OFFSYNC </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>미디어 시퀀스 번호가 이 MBR의 모든 HLS 스트림에서 동기화되지 않았습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170006 </span> </td> 
   <td colname="2"><span class="codeph"> MISSING_FILE_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명 </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>파일이 없거나 응답하지 않습니다. </p> <p>HTTP 404:파일을 찾을 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170007 </span> </td> 
   <td colname="2"><span class="codeph"> AD_EMPTY_RESPONSE </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>광고를 검색할 수 없습니다. 빈 응답입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TIMEOUT </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>광고를 검색할 수 없습니다. 시간 초과 오류입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170009 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> <p>자막 트랙을 변경하는 동안 오류가 발생했습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170010 </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_ERROR </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> 설명 </span> </td> 
   <td colname="5"> <p>SiteCatalyst 오류입니다. 설명을 참조하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170011 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TARGET_DURATION_INCOMPATIBLE </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>광고의 타겟 지속 시간이 컨텐츠의 타겟 지속 기간보다 높습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID 및 소스(URL)는 `PTAdAsset` `AD_ASSET` 키와 함께 알림 메타데이터의 을 통해 검색할 수 있습니다.
>
>이 `[]` 속성은 알림에 대한 선택적 키를 지정합니다.
