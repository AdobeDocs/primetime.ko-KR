---
description: GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 직접 비디오를 처리할 수 있습니다.
title: StageVideo 최소 요구 사항
exl-id: f401682d-c47d-4284-8832-293515a76581
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# StageVideo 최소 요구 사항{#stagevideo-minimum-requirements}

GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 직접 비디오를 처리할 수 있습니다.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

다양한 요소의 조합이 사용 가능한 시기와 방법을 결정합니다 `StageVideo`. 다음 표에서는 StageVideo 사용과 관련된 일부 요구 사항 및 제한 사항에 대한 스냅숏을 보여 줍니다. 이러한 요구 사항과 제한 사항은 변경될 수 있습니다.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 플랫폼 </th> 
   <th colname="col2" class="entry"> Windows 및 Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash 플레이어 </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">최소 Flash 10.1 이상 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">소프트웨어 대체 기능의 경우 Flash 15 이상 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">브라우저 및 <span class="codeph"> wmode</span> 설정 </td> 
   <td colname="col2"> <p><b>Flash 15에서</b>, 설정됨 <span class="codeph"> wmode=opaque</span> 따라서 HTML 오버레이를 사용할 수 있습니다. </p> <p>다음 브라우저는 현재 하드웨어 가속을 지원하지 않습니다. 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows의 Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome 26 이전 버전 및 Windows XP 및 Vista의 모든 Chrome 버전 </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer(모든 버전) </li> 
     </ul>다른 브라우저/OS 조합은 하드웨어 가속화에 대한 액세스를 방해할 수 있습니다. 이러한 시나리오에서는 <span class="codeph"> StageVideo</span> 성능에 부정적인 영향을 미치는 소프트웨어로 돌아갑니다. </p> <p><b>Flash 14 및 이전</b>, 브라우저가 하드웨어 가속을 지원하지 않는 경우 Flash 플레이어를 GPU에 직접 렌더링할 수 있지만 설정할 수 있습니다 <span class="codeph"> wmode=direct</span> 이 렌더링을 활성화합니다. <p>팁: 2009년 이전의 GPU 드라이버는 하드웨어 가속을 지원하지 않을 수 있으므로 업데이트해야 할 수 있습니다. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream 개체 </td> 
   <td colname="col2">다음 <span class="codeph"> StageVideoEvent.RENDER_STATE</span> 이벤트를 발송하지 않으려면 <span class="codeph"> NetStream</span> 에 대한 오브젝트 <span class="codeph"> StageVideo</span> 개체. </td> 
  </tr> 
 </tbody> 
</table>
