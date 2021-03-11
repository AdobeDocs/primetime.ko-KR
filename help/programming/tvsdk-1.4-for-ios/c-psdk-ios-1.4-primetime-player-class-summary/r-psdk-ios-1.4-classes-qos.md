---
description: 이러한 클래스는 플레이어의 성능을 확인하는 데 도움이 되는 정보를 제공합니다.
title: QoS 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# QoS 클래스{#qos-classes}

이러한 클래스는 플레이어의 성능을 확인하는 데 도움이 되는 정보를 제공합니다.

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이름 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
   <td colname="2">TVSDK가 실행되는 플랫폼 및 운영 체제에 대한 정보를 제공합니다. 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">플랫폼 OS 버전 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">TVSDK 라이브러리의 버전 번호 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">장치의 모델 이름 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">장치 제조업체 이름 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">장치 UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">장치 화면의 너비/높이 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> 재생의 성능에 대한 정보를 제공합니다. 여기에는 프레임 속도, 프로필 비트 전송률, 버퍼링에서 보낸 총 시간, 버퍼링 시도 횟수, 첫 번째 비디오 조각의 첫 번째 바이트를 가져오는 데 걸린 시간, 첫 번째 프레임을 렌더링하는 데 걸린 시간, 현재 버퍼링된 길이 및 버퍼 시간이 포함됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
   <td colname="2">
    <pre>
      재생과 장치 모두에 필요한 QoS 지표를 제공합니다.
    </pre>
    <pre>
      QOS 정보 공급자 클래스입니다.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>

