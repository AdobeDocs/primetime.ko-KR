---
description: GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 직접 비디오를 처리할 수 있습니다.
seo-description: GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 직접 비디오를 처리할 수 있습니다.
seo-title: 스테이지 비디오 최소 요구 사항
title: 스테이지 비디오 최소 요구 사항
uuid: 8916dbac-33e0-4efd-8105-9ddbc85f0a3f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 스테이지 비디오 최소 요구 사항{#stagevideo-minimum-requirements}

GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 직접 비디오를 처리할 수 있습니다.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

여러 가지 요인의 결합은 언제 어떻게 사용할 수 있는지 결정합니다 `StageVideo`. 다음 표는 StageVideo 사용과 관련된 몇 가지 요구 사항 및 제한 사항의 스냅숏을 제공합니다. 이러한 요구 사항 및 제한 사항은 변경될 수 있습니다.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 플랫폼 </th> 
   <th colname="col2" class="entry"> Windows 및 Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash Player </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Flash 10.1 이상 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">소프트웨어 기능에 대한 폴백, Flash 15 이상 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">브라우저 및 <span class="codeph"> wmode</span> 설정 </td> 
   <td colname="col2"> <p><b>Flash 15에서</b>wmode=opaque <span class="codeph"> 를</span> 설정하여 HTML 오버레이를 사용할 수 있습니다. </p> <p>다음 브라우저는 현재 하드웨어 가속을 지원하지 않습니다. 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows 기반의 Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Windows XP 및 Vista 기반의 Google Chrome 26 이전 및 모든 버전의 Chrome </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer(모든 버전) </li> 
     </ul>다른 브라우저/OS 조합으로 인해 하드웨어 가속을 이용할 수 없습니다. 이러한 시나리오에서 StageVideo <span class="codeph"> 는</span> 성능에 부정적인 영향을 미치는 상태로 다시 소프트웨어로 돌아갑니다. </p> <p><b>Flash 14 및 이전</b>버전에서 브라우저가 하드웨어 가속을 지원하지 않는 경우 Flash Player는 GPU로 직접 렌더링할 수 있지만 이 렌더링을 사용하도록 wmode=direct <span class="codeph"></span> 를 설정할 수 있습니다. <p>팁: 이러한 드라이버가 하드웨어 가속을 지원하지 않을 수 있으므로 2009년 이전의 GPU 드라이버를 업데이트해야 할 수 있습니다. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream 객체 </td> 
   <td colname="col2">StageVideoEvent <span class="codeph"> .RENDER_STATE</span> 이벤트는 StageVideo <span class="codeph"> 객체에 NetStream</span> 객체를 첨부하지 않는 한 <span class="codeph"> 전달되지</span> 않습니다. </td> 
  </tr> 
 </tbody> 
</table>

