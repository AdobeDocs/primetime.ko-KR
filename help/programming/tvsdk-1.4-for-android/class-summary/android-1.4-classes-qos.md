---
description: 이러한 클래스는 플레이어가 얼마나 성과가 있는지 확인하는 데 도움이 되는 정보를 제공합니다.
title: Qos 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Qos 클래스 {#qos-classes}

이러한 클래스는 플레이어가 얼마나 성과가 있는지 확인하는 데 도움이 되는 정보를 제공합니다.

패키지: [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/package-summary.html)  패키지: [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이름 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> 버퍼링 메트릭</a></span></td> 
   <td colname="2"> 플레이어에서 버퍼링하는 동안 소요한 시간과 버퍼링 이벤트가 발생한 빈도에 대한 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> 장치 정보</a> </span></td> 
   <td colname="2">구문이 실행되는 플랫폼 및 운영 체제에 대한 정보를 제공합니다. 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">플랫폼 OS 버전 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">구 라이브러리의 버전 번호 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">장치의 모델 이름 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">장치 제조업체 이름 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">장치 UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">장치 화면의 너비/높이 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/LoadInfo.html" format="html" scope="external"> LoadInfo</a></span> </td> 
   <td colname="2"> 다양한 리소스(파일, 매니페스트 또는 재생 목록, 조각/세그먼트, 트랙 등) 로드에 대한 다양한 QoS 정보가 포함되어 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> 재생 정보</a></span> </td> 
   <td colname="2"> 재생 수행 방법에 대한 정보를 제공합니다. 이는 프레임 레이트, 프로필 비트 레이트, 버퍼링에 소요된 총 시간, 버퍼링 시도 횟수, 제1 비디오 조각으로부터 제1 바이트를 얻는 데 걸린 시간, 제1 프레임을 렌더링하는 데 걸린 시간, 현재 버퍼링된 길이, 버퍼 시간을 포함한다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> 미디어를 로드하는 데 걸린 시간, 플레이어가 첫 번째 프레임을 렌더링하는 데 걸린 시간 또는 오류가 발생한 경우 실패하는 데 걸린 시간에 대한 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> 재생 지표</a> </span></td> 
   <td colname="2"> 재생이 작동하는 방식에 대한 정보를 제공합니다. 여기에는 프레임 레이트, 비트 레이트, 버퍼 길이 등이 포함됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">지표.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> 재생 세션 지표</a></span> </td> 
   <td colname="2"> 플레이어가 실제로 플레이하는 동안 소요한 시간(초)과 비디오가 실제로 화면에 표시되던 시간에 대한 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span></td> 
   <td colname="2">재생과 장치 모두에 필요한 QoS 지표를 제공합니다. QOS 정보 공급자 클래스입니다.</td> 
  </tr> 
 </tbody> 
</table>
