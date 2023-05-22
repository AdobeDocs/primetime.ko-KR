---
title: PSDK 오류 코드
description: 다양한 오류 코드, 경고 및 네이티브 오류 코드에 대한 정보입니다.
exl-id: 90d66c13-c40c-4602-83da-186c2b623375
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 6%

---

# PSDK 오류 코드 {#psdk-error-codes}

PSDK 오류 코드, 경고 및 네이티브 오류 코드에 대해 알아보려면 계속 읽으십시오.

## 오류

다음 표는 오류 유형 알림에 대한 자세한 정보를 제공합니다. 대부분의 오류에는 관련 메타데이터(예: 다운로드하지 못한 리소스의 URL)가 포함되어 있습니다. 일부 알림에는 기본 비디오 콘텐츠, 대체 오디오 콘텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함됩니다.

<table frame="all" colsep="1" rowsep="1">
  <tr> 
   <th><b>PSDK 오류 이름</b></th>
   <th><b>PSDK 오류 코드</b></th>
   <th><b>설명</b></th>
  </tr>
  <tr>
    <td>성공</td>
    <td>0</td>
    <td>기본 API에서 수행한 작업이 성공했습니다.</td>
  </tr>
  <tr>
    <td>잘못된 인수</td>
    <td>1</td>
    <td>기본 API에 제공된 데이터 또는 인수 형식이 잘못되었습니다.</td>
  </tr>
  <tr>
    <td>NULL_포인터</td>
    <td>2</td>
    <td>전달된 인수 중 하나가 NULL이거나 내부 구성원 중 하나가 초기화되지 않았습니다.</td>
  </tr>
  <tr>
    <td>ILLEGAL_STATE</td>
    <td>3</td>
    <td>작업이 현재 플레이어 상태에서 지원되지 않습니다.</td>
  </tr>
  <tr>
    <td>INTERFACE_NOT_FOUND</td>
    <td>4</td>
    <td>요청한 인터페이스가 이에 의해 구현/상속되지 않은 경우 interfaceCast 메서드에서 이 오류가 발생합니다.</td>
  </tr>
  <tr>  
    <td>CREATION_FAILED</td>
    <td>5</td>
    <td>내부 리소스 중 하나를 만들지 못했습니다.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_OPERATION</td>
    <td>6</td>
    <td>요청한 작업은 현재 지원되지 않습니다.</td>
  </tr>
  <tr>
    <td>DATA_NOT_AVAILABLE</td>
    <td>7</td>
    <td>요청한 데이터는 현재 사용할 수 없습니다.</td>
  </tr>
  <tr>
    <td>찾기 오류</td>
    <td>8</td>
    <td>찾기 작업을 수행하는 동안 오류가 발생했습니다.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_FEATURE</td>
    <td>9</td>
    <td>이 기능/기능은 지원되지 않습니다.</td>
  </tr>
  <tr>
    <td>범위 오류</td>
    <td>10</td>
    <td>지정한 값이 범위를 벗어났습니다.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORT</td>
    <td>11</td>
    <td>해당 스트림의 오디오/비디오 코덱이 TVSDK 또는 기본 장치에서 지원되지 않습니다.</td>
  </tr>
  <tr>
    <td>MEDIA_오류</td>
    <td>12</td>
    <td>지정한 미디어를 찾을 수 없습니다.</td>
  </tr>
  <tr>
    <td>네트워크 오류</td>
    <td>13</td>
    <td>조각 또는 세그먼트(비디오와 오디오 모두)를 다운로드하는 동안 오류가 발생했습니다.</td>
  </tr>
  <tr>
    <td>일반_오류</td>
    <td>14</td>
    <td>일반 오류 이벤트. 실제로 TVSDK에서 발급하지 않았습니다. 이것은 TVSDK 오류 이벤트에 대응하는 숫자 코드 범위의 끝에 대한 마커일 뿐입니다.</td>
  </tr>
  <tr>
    <td>INVALID_SEARCH_TIME</td>
    <td>15</td>
    <td>입력한 검색 시간이 잘못되었습니다.</td>
  </tr>
  <tr>
    <td>AUDIO_TRACK_ERROR</td>
    <td>16</td>
    <td>오디오 트랙과 관련된 오류가 발생했습니다(대체 오디오).</td>
  </tr>
  <tr>
    <td>ACCESS_FROM_DIFFERENT_THREAD</td>
    <td>17</td>
    <td>PSDK API는 PSDK가 초기화된 스레드와 다른 스레드에서 호출됩니다.</td>
  </tr>
  <tr>
    <td>ELEMENT_NOT_FOUND</td>
    <td>18</td>
    <td>요소를 찾을 수 없습니다.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>19</td>
    <td>기능이 구현되지 않았습니다.</td>
  </tr>
  <tr>
    <td>PRE_ROLL_DISABLED</td>
    <td>20</td>
    <td>AdvertisingMetadata를 통해 프리롤이 비활성화되었습니다.</td>
  </tr>
  <tr>
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>Flash Player에서 HLS 재생이 활성화되지 않았습니다. AuthorizedFeatures.enableMediaPlayerHLSPlayback() 을 참조하십시오.</td>
  </tr>
  <tr>
    <td>NETWORK_TIME</td>
    <td>58</td>
    <td>리소스/연결 서버를 가져오는 동안 네트워크 시간이 초과되었습니다.</td>
  </tr>
</table>

## 경고

다음 표는 WARN 유형 알림에 대한 자세한 정보를 제공합니다.
대부분의 경고에는 관련 메타데이터(예: 다운로드하지 못한 리소스의 URL)가 포함되어 있습니다. 일부 알림에는 기본 비디오 콘텐츠, 대체 오디오 콘텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함됩니다.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>오류 이름</b></th>
    <th><b>코드</b></th>
    <th><b>설명</b></th>
  </tr>
  <tr>
    <td>PLAYBACK_OPERATION_FAILED</td>
    <td>200</td>
    <td>재생 작업 도중 오류가 발생했습니다. 재생 관련 작업이 실패했습니다.</td>
  </tr>
  <tr>  
    <td>NATIVE_ALERT</td>
    <td>201</td>
    <td>낮은 수준의 AVE 라이브러리에서 오류가 발생했습니다.</td>
  </tr>
  <tr>
    <td>AD_RESOLVER_FAILED</td>
    <td>202</td>
    <td>광고 플러그인으로 광고를 해결하지 못했습니다.</td>
  </tr>
  <tr>
    <td>AD_MANIFEST_LOAD_FAILED</td>
    <td>203</td>
    <td>광고 매니페스트를 로드하지 못했습니다.</td>
  </tr>
  <tr>
    <td>AD_RESOLUTION_IN_PROGRESS</td>
    <td>204</td>
    <td>광고 해결 작업이 진행 중입니다.</td>
  </tr>
  </table>

## 정보

<table frame="all" colsep="1" rowsep="1">
  <tr> 
    <th><b>오류 이름</b></th>
    <th><b>코드</b></th>
    <th><b>설명</b></th>
  </tr>
  <tr>
    <td>REVENUE_OPTIMIZATION_REPORTING</td>
    <td>300</td>
    <td>추가 보고 및 분석을 위한 TVSDK 세부 알림.</td>
  </tr>
 </table>

## 네이티브 오류 코드

AVE의 비디오 인코더 인터페이스는 NATIVE_ERROR 메타데이터 객체에서 이러한 비디오 재생 통지를 반환한다.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>오류 이름</b></th>
    <th><b>코드</b></th>
    <th><b>설명</b></th>
  </tr>
  <tr>  
    <td>END_OF_PERIOD</td>
    <td>-1</td>
    <td>기간 종료.</td>
  </tr>
  <tr>
    <td>성공</td>
    <td>0</td>
    <td>작업이 완료되었습니다.</td>
  </tr>
  <tr>
    <td>ASYNC_OPERATION_IN_PROGRESS</td>
    <td>1</td>
    <td>비동기 작업. 작업 요청이 수행되었습니다. 성공/실패 정보는 나중에 사용할 수 있습니다.</td>
  </tr>
  <tr>
    <td>EOF</td>
    <td>2</td>
    <td>EOF(파일 끝) 조건으로 인해 작업을 수행할 수 없습니다.</td>
  </tr>
  <tr>
    <td>DECODER_FAILED</td>
    <td>3</td>
    <td>런타임에 디코더가 실패했습니다.</td>
  </tr>
  <tr>
    <td>DEVICE_OPEN_ERROR</td>
    <td>4</td>
    <td>하드웨어 디코더를 열지 못했습니다.</td>
  </tr>
  <tr>
    <td>파일 없음_찾음</td>
    <td>5</td>
    <td>리소스를 찾을 수 없습니다.</td>
  </tr>
  <tr>
    <td>일반_오류</td>
    <td>6</td>
    <td>일반 오류입니다.</td>
  </tr>
  <tr>
    <td>복구할 수 없음 오류</td>
    <td>7</td>
    <td>비디오 엔진에서 복구할 수 없는 오류 조건입니다.</td>
  </tr>
  <tr>
    <td>LOST_CONNECTION_RECOVERY</td>
    <td>8</td>
    <td>네트워크 오류입니다. 복구를 시도하고 있습니다.</td>
  </tr>
  <tr> 
    <td>NO_FIXED_SIZE</td>
    <td>9</td>
    <td>리소스의 크기를 결정할 수 없습니다.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>10</td>
    <td>기능이 구현되지 않았습니다.</td>
  </tr>
  <tr>
    <td>메모리 부족</td>
    <td>11</td>
    <td>메모리가 부족합니다.</td>
  </tr>
  <tr>
    <td>구문 분석 오류</td>
    <td>12</td>
    <td>미디어 파일을 구문 분석하는 중 오류가 발생했습니다.</td>
  </tr>
  <tr>  
    <td>SIZE_알 수 없음</td>
    <td>13</td>
    <td>리소스의 크기가 있지만 알 수 없습니다.</td>
  </tr>
  <tr>  
    <td>UNDER_FLOW</td>
    <td>14</td>
    <td>언더플로우 상태.</td>
  </tr>
  <tr> 
    <td>UNSUPPORTED_CONFIG</td>
    <td>15</td>
    <td>구성이 지원되지 않습니다.</td>
  </tr>
  <tr>  
    <td>UNSUPPORTED_OPERATION</td>
    <td>16</td>
    <td>작업이 지원되지 않습니다.</td>
  </tr>
  <tr>
    <td>WAITING_FOR_INIT</td>
    <td>17</td>
    <td>아직 초기화되지 않았습니다.</td>
  </tr>
  <tr>  
    <td>INVALID_PARAMETER</td>
    <td>18</td>
    <td>잘못된 매개변수.</td>
  </tr>
  <tr>
    <td>INVALID_OPERATION</td>
    <td>19</td>
    <td>작업이 허용되지 않았습니다.</td>
  </tr>
  <tr>
    <td>OP_ONLY_ALLOWED_IN_PAUSED_STATE</td>
    <td>20</td>
    <td>일시 중지된 동안에만 작업이 허용됩니다.</td>
  </tr>
  <tr> 
    <td>OP_INVALID_WITH_AUDIO_ONLY_FILE</td>
    <td>21</td>
    <td>오디오 전용 파일에는 작업을 사용할 수 없습니다.</td>
  </tr>
  <tr>
    <td>PREVIOUS_STEP_SEEK_IN_PROGRESS</td>
    <td>22</td>
    <td>이전 찾기 작업이 아직 진행 중입니다.</td>
  </tr>
  <tr> 
    <td>SOURCE_NOT_SPECIFIED</td>
    <td>23</td>
    <td>리소스를 지정하지 않았습니다.</td>
  </tr>
  <tr>
    <td>범위 오류</td>
    <td>24</td>
    <td>지정한 값이 범위를 벗어났습니다.</td>
  </tr>
  <tr>
    <td>INVALID_SEARCH_TIME</td>
    <td>25</td>
    <td>잘못된 검색 시간.</td>
  </tr>
  <tr>
    <td>FILE_STRUCTURE_INVALID</td>
    <td>26</td>
    <td>지정한 파일이 예상 구문을 준수하지 않습니다.</td>
  </tr>
  <tr>
    <td>COMPONENT_CREATION_FAILURE</td>
    <td>27</td>
    <td>필수 구성 요소를 만들 수 없습니다.</td>
  </tr>
  <tr>
    <td>DRM_INIT_ERROR</td>
    <td>28</td>
    <td>DRM 컨텍스트를 만들지 못했습니다.</td>
  </tr>
  <tr>
    <td>CONTAINER_NOT_SUPPORTED</td>
    <td>29</td>
    <td>컨테이너 유형이 지원되지 않습니다.</td>
  </tr>
  <tr>
    <td>SEEK_FAILED</td>
    <td>30</td>
    <td>찾기에 실패했습니다.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORT</td>
    <td>31</td>
    <td>지원되지 않는 코덱입니다.</td>
  </tr>
  <tr>
    <td>NETWORK_UNAVAILABLE</td>
    <td>32</td>
    <td>네트워크를 사용할 수 없습니다.</td>
  </tr>
  <tr>  
    <td>네트워크 오류</td>
    <td>33</td>
    <td>네트워크에서 데이터를 가져오는 도중 오류 발생.</td>
  </tr>
  <tr>
    <td>오버플로</td>
    <td>34</td>
    <td>오버플로입니다.</td>
  </tr>
  <tr>  
    <td>VIDEO_PROFILE_NOT_SUPPORTED</td>
    <td>35</td>
    <td>지원되지 않는 비디오 프로필입니다.</td>
  </tr>
  <tr>
    <td>PERIOD_NOT_LOADED</td>
    <td>36</td>
    <td>보류 기간 또는 아직 로드되지 않은 기간에 작업을 시도했습니다.</td>
  </tr>
  <tr> 
    <td>INVALID_REPLACE_DURATION</td>
    <td>37</td>
    <td>지정한 바꾸기 기간이 잘못되었거나 스트림의 끝을 지나 확장되었습니다.</td>
  </tr>
  <tr>
    <td>CALLED_FROM_WRONG_THREAD</td>
    <td>38</td>
    <td>잘못된 스레드에서 API를 호출할 수 없습니다. 대부분, 기본 스레드에서만 호출해야 하는 API 요소의 경우.</td>
  </tr>
  <tr>
    <td>FRAGMENT_READ_오류</td>
    <td>39</td>
    <td>조각 읽기 오류. 장애 조치(failover)가 없습니다. 엔진은 다음 조각을 읽으려고 시도합니다.</td>
  </tr>
  <tr>
    <td>중단됨</td>
    <td>40</td>
    <td>명시적 Abort 또는 Destroy 호출에 의해 작업이 중단되었습니다.</td>
  </tr>
  <tr>
    <td>지원되지 않는 HLS_VERSION</td>
    <td>41</td>
    <td>이 버전의 HLS 미디어를 재생할 수 없습니다.</td>
  </tr>
  <tr>
    <td>CANNOT_FAIL_OVER</td>
    <td>42</td>
    <td>장애 조치(failover)할 수 없습니다.</td>
  </tr>
  <tr> 
    <td>HTTP_TIME_OUT</td>
    <td>43</td>
    <td>HTTP 다운로드 시간이 초과되었습니다.</td>
  </tr>
  <tr>
    <td>NETWORK_DOWN</td>
    <td>44</td>
    <td>사용자의 네트워크 연결이 끊어졌습니다. 재생은 언제든지 중단될 수 있으며 연결을 사용할 수 있을 때 다시 시작됩니다.</td>
  </tr>
  <tr>
    <td>NO_USABLE_BITRATE_PROFILE</td>
    <td>45</td>
    <td>스트림에 사용 가능한 비트 전송률 프로필이 없습니다.</td>
  </tr>
  <tr>
    <td>BAD_MANIFEST_SIGNATURE</td>
    <td>46</td>
    <td>매니페스트의 서명이 잘못되었습니다. 매니페스트 서명 테스트에 실패했습니다.</td>
  </tr>
  <tr>
    <td>CANNOT_LOAD_PLAYLIST</td>
    <td>47</td>
    <td>재생 목록을 로드할 수 없습니다.</td>
  </tr>
  <tr>
    <td>REPLACEMENT_FAILED</td>
    <td>48</td>
    <td>삽입 API에 지정된 대체를 수행할 수 없습니다. 삽입은 성공했지만 교체는 성공하지 못했다는 의미다. 대체할 매니페스트가 타임라인에서 제거된 경우 교체가 실패할 수 있습니다.</td>
  </tr>
  <tr>
    <td>SWITCH_TO_ASYMMETRIC_PROFILE</td>
    <td>49</td>
    <td>DRM이 비대칭 프로파일로 전환되고 있습니다. 모든 프로필은 기간이 일치해야 합니다. 그렇지 않으면 이 경고가 표시되고 재생에서 점프가 있을 수 있습니다.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_BACKWARD</td>
    <td>50</td>
    <td>라이브 창은 앞으로 이동해야 합니다. 그렇지 않으면 이 경고가 표시되고 창이 읽히지 않습니다. 이로 인해 재생에서 점프(또는 정지/긴 일시 중지)가 있을 수 있습니다.</td>
  </tr>
  <tr>
    <td>CURRENT_PERIOD_EXPIRED</td>
    <td>51</td>
    <td>라이브 창이 현재 기간 이상으로 이동되었습니다.</td>
  </tr>
  <tr>
    <td>CONTENT_LENGTH_MISMATCH</td>
    <td>52</td>
    <td>HTTP 서버에서 보고한 콘텐츠 길이가 실제 미디어 크기와 일치하지 않습니다.</td>
  </tr>
  <tr>
    <td>기간 보류</td>
    <td>53</td>
    <td>setHoldAt API에서 설정한 시간에 도달했기 때문에 미디어 판독기에서 더 이상 읽을 수 없습니다.</td>
  </tr>
  <tr>  
    <td>LIVE_HOLD</td>
    <td>54</td>
    <td>라이브 창의 끝에 도달했으므로 미디어 판독기에서 세그먼트를 로드할 수 없습니다. 서버가 새 미디어를 라이브 창에 광고하면 세그먼트 로드가 다시 시작됩니다. 이 상태는 일반적으로 다음과 같은 경우에 도달합니다.<ul><li>bufferTime이 너무 높습니다(라이브 창 기간과 같거나 그보다 높음).</li><li>삽입/지우기 API 중 하나 이상의 조합이 추가된 미디어보다 더 많은 미디어를 대체했습니다.</li><li>다음 기간은 InsertBy API 호출로 인해 미디어 교체가 보류 중인 라이브 기간입니다</li></ul></td>
  </tr>
  <tr>
    <td>BAD_MEDIA_INTERLEAVING</td>
    <td>55</td>
    <td>미디어의 오디오 및 비디오 인터리빙이 제대로 수행되지 않습니다. 패키징 오류입니다. 차이가 2초를 초과하면 경고가 발송됩니다.</td>
  </tr>
  <tr>
    <td>DRM_NOT_AVAILABLE</td>
    <td>56</td>
    <td></td>
  </tr>
  <tr>  
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>Flash Player에서 HLS 재생이 활성화되지 않았습니다. AuthorizedFeatures.enableHLSPlayback을 참조하십시오.</td>
  </tr>
  <tr>
    <td>BAD_MEDIA_SAMPLE_FOUND</td>
    <td>58</td>
    <td>디코더가 디코딩할 수 없는 잘못된 샘플을 받았습니다. 이는 일반적으로 치명적인 오류는 아니지만 오디오/비디오에 결함이 있을 수 있음을 나타냅니다. 이 오류의 인스턴스가 너무 많으면 인코딩이나 파일이 잘못되었음을 나타냅니다.</td>
  </tr>
  <tr>
    <td>RANGE_SPANS_READ_HEAD</td>
    <td>59</td>
    <td>재생이 시작된 후 삽입/바꾸기 범위에 읽기 헤드가 포함되지 않아야 합니다.</td>
  </tr>
  <tr> 
    <td>POSTROLL_WITH_LIVE_NOT_ALLOWED</td>
    <td>60</td>
    <td>포스트롤 삽입은 라이브 미디어에서 허용되지 않습니다. 그러나 서버에서 미디어를 완료된 것으로 표시한 후에는 허용됩니다.</td>
  </tr>
  <tr>
    <td>내부 오류</td>
    <td>61</td>
    <td>결코 일어나서는 안 되는 아주 드문 문제이다.</td>
  </tr>
  <tr>  
    <td>SPS_PPS_FOUND_OUTSIDE_AVCC</td>
    <td>62</td>
    <td>스트림은 항상 AVCC에 H264 SPS/PPS를 넣는 패키징 권장 사항을 따르지 않습니다. 찾기/재생 문제가 표시될 수 있습니다.</td>
  </tr>
  <tr>  
    <td>PARTIAL_REPLACEMENT</td>
    <td>63</td>
    <td>Insert API에 지정된 교체는 일부만 수행되었습니다. replaceDuration이 타임라인 지속 시간 전체에 걸쳐 있는 경우 이 문제가 발생합니다.</td>
  </tr>
  <tr>
    <td>RENDITION_M3U8_ERROR</td>
    <td>64</td>
    <td>렌디션 재생 목록을 로드하는 도중 오류가 발생했습니다. 이 기능은 AVE에만 해당되며 FlashPlayer에는 해당되지 않습니다.</td>
  </tr>
  <tr>
    <td>작업 없음</td>
    <td>65</td>
    <td>작업이 아무 작업도 수행하지 않습니다.</td>
  </tr>
  <tr>
    <td>SEGMENT_SKIPPED_ON_FAILURE</td>
    <td>66</td>
    <td>세그먼트는 재생할 수 없으며 실패 시 건너뜁니다.</td>
  </tr>
  <tr>
    <td>호환되지 않는_RENDER_MODE</td>
    <td>67</td>
    <td>호환되지 않는 렌더링 모드입니다.</td>
  </tr>
  <tr>
    <td>PROTOCOL_NOT_SUPPORT</td>
    <td>68</td>
    <td>URL에 사용된 웹 프로토콜은 지원되지 않습니다.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR_INCOMPATIBLE_VERSION</td>
    <td>69</td>
    <td>미디어 파일을 구문 분석하는 중 오류가 발생했습니다.</td>
  </tr>
  <tr>  
    <td>MANIFEST_FILE_UNEXPECTED_CHANGED</td>
    <td>70</td>
    <td>매니페스트 파일이 예기치 않은 방식으로 변경되었습니다.</td>
  </tr>
  <tr>
    <td>CANNOT_SPLIT_TIMELINE</td>
    <td>71</td>
    <td>타임라인에서 분할 작업을 수행할 수 없습니다.</td>
  </tr>
  <tr>
    <td>CANNOT_ERASE_TIMELINE</td>
    <td>72</td>
    <td>타임라인에서 지우기 작업을 수행할 수 없습니다.</td>
  </tr>
  <tr>
    <td>DID_NOT_GET_NEXT_FRAGMENT</td>
    <td>73</td>
    <td>다음 조각을 가져오지 못했습니다.</td>
  </tr>
  <tr>
    <td>NO_TIMELINE</td>
    <td>74</td>
    <td>내부 데이터 구조에 타임라인이 없습니다.</td>
  </tr>
  <tr>
    <td>LISTENER_NOT_FOUND</td>
    <td>75</td>
    <td>내부 데이터 구조에 수신기가 없습니다.</td>
  </tr>
  <tr>
    <td>AUDIO_START_ERROR</td>
    <td>76</td>
    <td>오디오를 시작할 수 없습니다.</td>
  </tr>
  <tr>
    <td>NO_AUDIO_SINK</td>
    <td>77</td>
    <td>내부 데이터 구조에 오디오 싱크가 없습니다.</td>
  </tr>
  <tr>  
    <td>FILE_OPEN_ERROR</td>
    <td>78</td>
    <td>파일을 열 수 없습니다.</td>
  </tr>
  <tr>
    <td>FILE_WRITE_ERROR</td>
    <td>79</td>
    <td>파일에 쓸 수 없습니다.</td>
  </tr>
  <tr>
    <td>FILE_READ_ERROR</td>
    <td>80</td>
    <td>파일에서 읽을 수 없습니다.</td>
  </tr>
  <tr>
    <td>ID3PARSE_ERROR</td>
    <td>81</td>
    <td>ID3 데이터를 구문 분석하는 도중 오류가 발생했습니다.</td>
  </tr>
  <tr>
    <td>SECURITY_ERROR</td>
    <td>82</td>
    <td>보안 제한으로 인해 콘텐츠를 로드하지 못했습니다.</td>
  </tr>
  <tr>
    <td>TIMELINE_TOO_SHORT</td>
    <td>83</td>
    <td>타임라인 기간이 너무 짧습니다. 라이브 스트림인 경우 버퍼링이 자주 발생할 수 있습니다.</td>
  </tr>
  <tr>
    <td>AUDIO_ONLY_STREAM_START</td>
    <td>84</td>
    <td>스트림이 오디오 전용 스트림으로 전환되었습니다.</td>
  </tr>
  <tr>  
    <td>AUDIO_ONLY_STREAM_END</td>
    <td>85</td>
    <td>스트림이 오디오 전용 스트림에서 비디오가 있는 스트림으로 전환되었습니다.</td>
  </tr>
  <tr>
    <td>키 없음_찾음</td>
    <td>87</td>
    <td>키를 찾을 수 없습니다.</td>
  </tr>
  <tr>
    <td>잘못된 키</td>
    <td>88</td>
    <td>키가 잘못되었습니다.</td>
  </tr>
  <tr>
    <td>KEY_SERVER_NOT_FOUND</td>
    <td>89</td>
    <td>키 서버가 키를 반환하지 않습니다.</td>
  </tr>
  <tr>
    <td>MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</td>
    <td>90</td>
    <td>기본 매니페스트 업데이트를 처리할 수 없습니다.</td>
  </tr>
  <tr>
    <td>UNREPORTED_TIME_DISCONTINUITY_FOUND</td>
    <td>91</td>
    <td>보고되지 않은 시간(PTS) 불연속성이 발견되었습니다.</td>
  </tr>
  <tr>
    <td>UNMATCHED_AV_DISCONTINUITY_FOUND</td>
    <td>92</td>
    <td>탁월한 오디오 및 비디오 불연속성이 발견되었습니다.</td>
  </tr>
  <tr>
    <td>TRICKPLAY_ENDED_DUE_TO_ERROR</td>
    <td>93</td>
    <td>트릭 재생 모드에서 미디어를 재생하는 동안 오류가 발생했습니다. 트릭 재생 모드가 종료되고 스트림이 일시 중지되었습니다. 일반 모드에서 미디어를 재생하려면 Play()를 호출하십시오.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_AHEAD</td>
    <td>95</td>
    <td>플레이어가 라이브 창을 벗어났으므로 따라잡기 위해 앞으로 나아가야 합니다.</td>
  </tr>
</table>
