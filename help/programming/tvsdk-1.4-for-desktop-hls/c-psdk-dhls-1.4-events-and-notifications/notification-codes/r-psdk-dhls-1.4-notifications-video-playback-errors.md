---
description: AVE의 비디오 인코더 인터페이스는 NATIVE_ERROR 메타데이터 객체에서 이러한 비디오 재생 통지를 반환한다.
title: NATIVE_ERROR 비디오 재생 값
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 6%

---

# NATIVE_ERROR: 비디오 재생 값{#native-error-video-playback-values}

AVE의 비디오 인코더 인터페이스는 NATIVE_ERROR 메타데이터 객체에서 이러한 비디오 재생 통지를 반환한다.

<table> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> RUNTIME_CODE 메타데이터 키 값 </th> 
   <th colname="col2" class="entry"> RUNTIME_CODE_MESSAGE 메타데이터 키 값 </th> 
   <th colname="col3" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> 기간 종료. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> 성공</span> </td> 
   <td colname="col3"> 작업이 완료되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> 비동기 작업. 작업 요청이 수행되었습니다. 성공/실패 정보는 나중에 사용할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> EOF(파일 끝) 조건으로 인해 작업을 수행할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> 런타임에 디코더가 실패했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 하드웨어 디코더를 열지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> 파일 없음_찾음 </span> </td> 
   <td colname="col3"> 리소스를 찾을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> 일반_오류 </span> </td> 
   <td colname="col3"> 일반 오류입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> 복구할 수 없음 오류 </span> </td> 
   <td colname="col3"> 비디오 엔진에서 복구할 수 없는 오류 조건입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERY </span> </td> 
   <td colname="col3"> 네트워크 오류입니다. 복구를 시도하고 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> 리소스의 크기를 결정할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED </span> </td> 
   <td colname="col3"> 기능이 구현되지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> 메모리 부족 </span> </td> 
   <td colname="col3"> 메모리가 부족합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> 구문 분석 오류 </span> </td> 
   <td colname="col3"> 미디어 파일을 구문 분석하는 중 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_알 수 없음 </span> </td> 
   <td colname="col3"> 리소스의 크기가 있지만 알 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> 언더플로우 상태. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG </span> </td> 
   <td colname="col3"> 구성이 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION </span> </td> 
   <td colname="col3"> 작업이 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> 아직 초기화되지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> 잘못된 매개변수. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> 작업이 허용되지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> 일시 중지된 동안에만 작업이 허용됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> 오디오 전용 파일에는 작업을 사용할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> 이전 찾기 작업이 아직 진행 중입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED </span> </td> 
   <td colname="col3"> 리소스를 지정하지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> 범위 오류</span> </td> 
   <td colname="col3"> 지정한 값이 범위를 벗어났습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEARCH_TIME</span> </td> 
   <td colname="col3"> 잘못된 검색 시간. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> 지정한 파일이 예상 구문을 준수하지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> 필수 구성 요소를 만들 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> DRM 컨텍스트를 만들지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> 컨테이너 유형이 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> 찾기에 실패했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORT</span> </td> 
   <td colname="col3"> 지원되지 않는 코덱입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> 네트워크를 사용할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> 네트워크 오류</span> </td> 
   <td colname="col3"> 네트워크에서 데이터를 가져오는 도중 오류 발생. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> 오버플로</span> </td> 
   <td colname="col3"> 오버플로입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 지원되지 않는 비디오 프로필입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> 보류 기간 또는 아직 로드되지 않은 기간에 작업을 시도했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> 지정한 바꾸기 기간이 잘못되었거나 스트림의 끝을 지나 확장되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> 잘못된 스레드에서 API를 호출할 수 없습니다. 대부분, 기본 스레드에서만 호출해야 하는 API 요소의 경우. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_오류</span> </td> 
   <td colname="col3"> 조각 읽기 오류. 장애 조치(failover)가 없습니다. 엔진은 다음 조각을 읽으려고 시도합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> 중단됨</span> </td> 
   <td colname="col3"> 명시적 Abort 또는 Destroy 호출에 의해 작업이 중단되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> 지원되지 않는 HLS_VERSION</span> </td> 
   <td colname="col3"> 이 버전의 HLS 미디어를 재생할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> 장애 조치(failover)할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP 다운로드 시간이 초과되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN </span> </td> 
   <td colname="col3"> 사용자의 네트워크 연결이 끊어졌습니다. 재생은 언제든지 중단될 수 있으며 연결을 사용할 수 있을 때 다시 시작됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> 스트림에 사용 가능한 비트 전송률 프로필이 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> 매니페스트의 서명이 잘못되었습니다. 매니페스트 서명 테스트에 실패했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> 재생 목록을 로드할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> 삽입 API에 지정된 대체를 수행할 수 없습니다. 삽입은 성공했지만 교체는 성공하지 못했다는 의미다. 대체할 매니페스트가 타임라인에서 제거된 경우 교체가 실패할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM이 비대칭 프로파일로 전환되고 있습니다. 모든 프로필은 기간이 일치해야 합니다. 그렇지 않으면 이 경고가 표시되고 재생에서 점프가 있을 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> 라이브 창은 앞으로 이동해야 합니다. 그렇지 않으면 이 경고가 표시되고 창이 읽히지 않습니다. 이로 인해 재생에서 점프(또는 정지/긴 일시 중지)가 있을 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> 라이브 창이 현재 기간 이상으로 이동되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> HTTP 서버에서 보고한 콘텐츠 길이가 실제 미디어 크기와 일치하지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> 기간 보류</span> </td> 
   <td colname="col3"> 미디어 판독기에서 설정한 시간에 도달했으므로 더 이상 읽을 수 없습니다. <span class="codeph"> setHoldAt</span> API. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3"> 라이브 창의 끝에 도달했으므로 미디어 판독기에서 세그먼트를 로드할 수 없습니다. 서버가 새 미디어를 라이브 창에 광고하면 세그먼트 로드가 다시 시작됩니다. 이 상태는 일반적으로 다음과 같은 경우에 도달합니다. 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">다음 <span class="codeph"> bufferTime</span> 이(가) 너무 높습니다(라이브 창 기간과 같거나 그보다 높음). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">삽입/지우기 API 중 하나 이상의 조합이 추가된 미디어보다 더 많은 미디어를 대체했습니다. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">다음 기간은 미디어 교체가 보류 중인 라이브 기간입니다( 로 인해) <span class="codeph"> 삽입 기준</span> API 호출) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> 미디어의 오디오 및 비디오 인터리빙이 제대로 수행되지 않습니다. 패키징 오류입니다. 차이가 2초를 초과하면 경고가 발송됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> Flash Player에서 HLS 재생이 활성화되지 않았습니다. 다음을 참조하십시오 <span class="codeph"> AuthorizedFeatures.enableHLSPlayback</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> 디코더가 디코딩할 수 없는 잘못된 샘플을 받았습니다. 이는 일반적으로 치명적인 오류는 아니지만 오디오/비디오에 결함이 있을 수 있음을 나타냅니다. 이 오류의 인스턴스가 너무 많으면 인코딩이나 파일이 잘못되었음을 나타냅니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> 재생이 시작된 후 삽입/바꾸기 범위에 읽기 헤드가 포함되지 않아야 합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> 포스트롤 삽입은 라이브 미디어에서 허용되지 않습니다. 그러나 서버에서 미디어를 완료된 것으로 표시한 후에는 허용됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> 내부 오류</span> </td> 
   <td colname="col3"> 결코 일어나서는 안 되는 아주 드문 문제이다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> 스트림은 항상 AVCC에 H264 SPS/PPS를 넣는 패키징 권장 사항을 따르지 않습니다. 찾기/재생 문제가 표시될 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> Insert API에 지정된 교체는 일부만 수행되었습니다. replaceDuration이 타임라인 지속 시간 전체에 걸쳐 있는 경우 이 문제가 발생합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> 렌디션 재생 목록을 로드하는 도중 오류가 발생했습니다. 이 기능은 AVE에만 해당되며 FlashPlayer에는 해당되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> 작업 없음</span> </td> 
   <td colname="col3"> 작업이 아무 작업도 수행하지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> 세그먼트는 재생할 수 없으며 실패 시 건너뜁니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> 호환되지 않는_RENDER_MODE</span> </td> 
   <td colname="col3"> 호환되지 않는 렌더링 모드입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORT </span> </td> 
   <td colname="col3"> URL에 사용된 웹 프로토콜은 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> 미디어 파일을 구문 분석하는 중 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTED_CHANGED</span> </td> 
   <td colname="col3"> 매니페스트 파일이 예기치 않은 방식으로 변경되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> 타임라인에서 분할 작업을 수행할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> 타임라인에서 지우기 작업을 수행할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> 다음 조각을 가져오지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> 내부 데이터 구조에 타임라인이 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> 내부 데이터 구조에 수신기가 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> 오디오를 시작할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> 내부 데이터 구조에 오디오 싱크가 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 파일을 열 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> 파일에 쓸 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> 파일에서 읽을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> ID3 데이터를 구문 분석하는 도중 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="col3"> 보안 제한으로 인해 콘텐츠를 로드하지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> 타임라인 기간이 너무 짧습니다. 라이브 스트림인 경우 버퍼링이 자주 발생할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> 스트림이 오디오 전용 스트림으로 전환되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> 스트림이 오디오 전용 스트림에서 비디오가 있는 스트림으로 전환되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> 키 없음_찾음 </span> </td> 
   <td colname="col3"> 키를 찾을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> 잘못된 키</span> </td> 
   <td colname="col3"> 키가 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> 키 서버가 키를 반환하지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> 기본 매니페스트 업데이트를 처리할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> 보고되지 않은 시간(PTS) 불연속성이 발견되었습니다. </td> 
  </tr> 
 </tbody> 
</table>
