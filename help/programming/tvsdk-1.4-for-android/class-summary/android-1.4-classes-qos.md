---
description: 이러한 클래스는 플레이어의 성능을 확인하는 데 도움이 되는 정보를 제공합니다.
seo-description: 이러한 클래스는 플레이어의 성능을 확인하는 데 도움이 되는 정보를 제공합니다.
seo-title: QoS 클래스
title: QoS 클래스
uuid: c1f0218d-4a79-4141-9a74-e70ac4f70aa5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# QoS 클래스 {#qos-classes}

이러한 클래스는 플레이어의 성능을 확인하는 데 도움이 되는 정보를 제공합니다.

패키지: [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/package-summary.html) 패키지: [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이름 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표를 참조하십시오.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> 버퍼링 지표</a></span></td> 
   <td colname="2"> 플레이어가 버퍼링 동안 보낸 시간 및 버퍼링 이벤트가 발생한 빈도에 대한 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> 장치 정보</a> </span></td> 
   <td colname="2">구문이 실행되는 플랫폼 및 운영 체제에 대한 정보를 제공합니다. 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">플랫폼 OS 버전 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">구문 라이브러리의 버전 번호 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">장치의 모델 이름 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">장치 제조업체 이름 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">장치 UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">장치 화면의 너비/높이 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/LoadInfo.html" format="html" scope="external"> LoadInfo</a></span> </td> 
   <td colname="2"> 다양한 리소스(파일, 매니페스트 또는 재생 목록, 조각/세그먼트, 트랙 등)를 로드하는 방법에 대한 다양한 QoS 정보를 포함합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> 재생 정보</a></span> </td> 
   <td colname="2"> 재생의 성능에 대한 정보를 제공합니다. 여기에는 프레임 속도, 프로필 비트 전송률, 버퍼링 시 소요된 총 시간, 버퍼링 시도 횟수, 첫 번째 비디오 조각에서 첫 번째 바이트를 얻는 데 걸린 시간, 첫 번째 프레임을 렌더링하는 데 걸린 시간, 현재 버퍼링 길이 및 버퍼 시간이 포함됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표를 참조하십시오.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> 미디어를 로드하는 데 걸린 시간, 플레이어가 첫 번째 프레임을 렌더링하는 데 걸린 시간 또는 오류가 발생한 경우 실패에 대한 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표를 참조하십시오.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackMetrics</a> </span></td> 
   <td colname="2"> 재생이 수행되는 방식에 대한 정보를 제공합니다. 여기에는 프레임 속도, 비트 속도, 버퍼 길이 등이 포함됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표를 참조하십시오.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> 플레이어가 실제로 재생하는 동안 보낸 시간(초) 및 비디오가 실제로 화면에 표시된 시간에 대한 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span></td> 
   <td colname="2">재생과 디바이스 모두에 필요한 QoS 지표를 제공합니다. QOS 정보 공급자 클래스입니다.</td> 
  </tr> 
 </tbody> 
</table>
