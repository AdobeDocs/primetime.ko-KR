---
description: 이러한 클래스는 미디어 플레이어 및 해당 리소스를 설명합니다.
seo-description: 이러한 클래스는 미디어 플레이어 및 해당 리소스를 설명합니다.
seo-title: 미디어 플레이어 클래스
title: 미디어 플레이어 클래스
uuid: 6b59dcff-9722-4a84-9049-f6f10f7b3e82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# 미디어 플레이어 클래스 {#media-player-classes}

Primetime Player Objective-C API를 사용하여 플레이어의 동작을 사용자 정의할 수 있습니다.

이러한 클래스는 미디어 플레이어 및 해당 리소스를 설명합니다.

<table frame="all" colsep="1" rowsep="1" id="table_bm2_wl2_2m"> 
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>클래스</b> </td> 
   <td colname="2"><b>설명</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTABRControlParameters.html" format="html" scope="external"> PTABRControlParameters</a></span> </td> 
   <td colname="2">모든 적응형 비트 전송률 제어 매개 변수를 캡슐화합니다. 지원되는 매개 변수는 다음과 같습니다. 
    <ul id="ul_pnh_hm2_2m"> 
     <li id="li_46572FE1EB514AFF8C9F731E44DAF30B"><span class="codeph"> minBitRate</span> </li> 
     <li id="li_A10C75C9A5234241A5B84A4139F4D143"><span class="codeph"> maxBitRate</span> </li> 
     <li id="li_4E77E367A2E848D2B3E1A9C52209A7B2"><span class="codeph"> initialBitRate</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDefaultMediaPlayerClientFactory.html" format="html" scope="external"> PTDefaultMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> TVSDK에서 <span class="codeph"> PTMediaPlayerClientFactory</span>의 기본 구현입니다. 사용 가능한 <span class="codeph"> PTOpportunityResolver</span>, <span class="codeph"> PTContentResolver</span> 및 <span class="codeph"> PTAdPolicySelector</span> 인스턴스를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html" format="html" scope="external"> PTMediaPlayer</a></span> </td> 
   <td colname="2">Primetime Player 프레임워크의 루트 구성 요소를 정의합니다. <p>응용 프로그램은 미디어를 재생하기 위해 이 클래스의 인스턴스를 만듭니다. 이 구성 요소는 알림을 전달하여 응용 프로그램에서 지정된 시간에 플레이어 상태를 알 수 있도록 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTMediaPlayerClientFactory.html" format="html" scope="external"> PTMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> 사용 가능한 <span class="codeph"> PTOpentunityResolver</span> , <span class="codeph"> PTContentResolver</span> 및 <span class="codeph"> PTAdPolicySelector</span> 인스턴스를 제공하기 위해 구현해야 하는 방법을 설명하는 프로토콜입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerItem.html" format="html" scope="external"> PTMediaPlayerItem</a></span> </td> 
   <td colname="2"> 특정 오디오-비디오 미디어를 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerView.html" format="html" scope="external"> PTMediaPlayerView</a></span> </td> 
   <td colname="2"> Primetime Player 프레임워크의 보기 구성 요소를 관리합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaProfile.html" format="html" scope="external"> PTMediaProfile</a></span> </td> 
   <td colname="2"> 변형 재생 목록에서 단일 스트림의 프로필을 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaSelectionOption.html" format="html" scope="external"> PTMediaSelectionOption</a></span> </td> 
   <td colname="2">서로 다른 언어 환경 설정, 액세서빌러티 요구 사항 또는 사용자 정의 응용 프로그램 구성을 수용하기 위한 오디오 비주얼 미디어 리소스를 나타냅니다. 유효한 옵션 유형: 
    <ul id="ul_p2q_gn2_2m"> 
     <li id="li_46BE5AE49732481FB6D336FFF896E5AD">자막 (<span class="codeph"> PTMediaSelectionOptionTypeSubtitle</span>) </li> 
     <li id="li_6CEADCA12D4A48B7AE4A539985F32119">대체 오디오(<span class="codeph"> PTMediaSelectionOptionTypeAudio</span>) </li> 
     <li id="li_248D3D997F8A4B6E9B48869F84060D1F"> <p>정의되지 않음(<span class="codeph"> PTMediaSelectionOptionTypeUndefined</span>) </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTOpportunityResolver.html" format="html" scope="external"> PTOpportunityResolverclass, </a> </span>   <span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolver.html" format="html" scope="external"> </a> PTOpportunityResolverprotocol</span> </td> 
   <td colname="2"> Adobe Primetime 광고 결정 프로세스에 배치로 사용될 매니페스트 내 큐를 처리하는 데 사용되는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolverDelegate.html" format="html" scope="external"> PTOpportunityResolverDelegate</a></span> </td> 
   <td colname="2"> 사용자 지정 기회 확인자( <span class="codeph"> PTOpportunityResolver</span> )가 기회 해결 상태를 대리인에게 전달하는 데 사용해야 하는 방법을 설명하는 프로토콜입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDK.html" format="html" scope="external"> PTSDK</a></span> </td> 
   <td colname="2"> TVSDK 버전 및 기능에 대해 설명합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDKConfig.html" format="html" scope="external"> PTSDKConfig</a></span> </td> 
   <td colname="2"> TVSDK 전역 설정을 표시하고 응용 프로그램이 사용자 정의 HLS 태그에 가입할 수 있도록 합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTextStyleRule.html" format="html" scope="external"> PTTextStyleRule</a></span> </td> 
   <td colname="2"> 규칙 사전을 구성하는 텍스트 스타일 속성 키를 나타내는 상수를 정의합니다. </td> 
  </tr> 
 </tbody> 
</table>

