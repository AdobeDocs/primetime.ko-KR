---
description: Primetime 플레이어 API를 사용하여 플레이어의 동작을 사용자 지정할 수 있습니다. 이러한 클래스는 미디어 플레이어와 해당 리소스를 설명합니다.
title: Mediacore 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---

# Mediacore 클래스{#mediacore-classes}

Primetime 플레이어 API를 사용하여 플레이어의 동작을 사용자 지정할 수 있습니다. 이러한 클래스는 미디어 플레이어와 해당 리소스를 설명합니다.

TVSDK에 대한 전체 API 설명서를 보려면 [Adobe Primetime API 참조](https://help.adobe.com/en_US/primetime/api/index.html).

이러한 클래스는 미디어 플레이어와 해당 리소스에 대해 설명합니다.
패키지: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>이름 </p> </th> 
   <th colname="2" class="entry"> <p>설명 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> ABRControlParameters</a> </span> </td> 
   <td colname="2"> 모든 적응형 비트 전송률 제어 매개 변수를 캡슐화하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> 버퍼 제어 매개변수</a></span> </td> 
   <td colname="2"> 모든 버퍼 제어 매개 변수를 캡슐화하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionStyles.html" format="html" scope="external"> 폐쇄 캡션 스타일</a></span> </td> 
   <td colname="2"> 폐쇄 캡션의 텍스트에 대한 모든 스타일 속성을 정의하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionsVisibility.html" format="html" scope="external"> ClosedCaptionsVisibility</a></span> </td> 
   <td colname="2"> 폐쇄 캡션의 표시 여부를 제어하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ContentFactory.html" format="html" scope="external"> ContentFactory</a> </span> </td> 
   <td colname="2"> 광고 워크플로에 사용되는 다양한 구성 요소를 만들고 관리하기 위한 기본 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> 광고 재생 동작에 대한 기본 구현입니다. 애플리케이션에서 광고 동작을 사용자 지정할 수 있는 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultContentFactory.html" format="html" scope="external"> DefaultContentFactory</a></span> </td> 
   <td colname="2">기본 구현 <span class="codeph"> MediaPlayerClient</span> 팩토리에서 메타데이터 및 광고 해결 프로세스를 모두 지원합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2">의 기본 클래스 구현 <span class="codeph"> MediaPlayer</span> 인터페이스. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerConfig.html" format="html" scope="external"> 기본 미디어 플레이어 구성</a> </span> </td> 
   <td colname="2"> 미디어 플레이어의 기본 구현을 위한 구성 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> 기본 미디어 플레이어 항목 구성</a></span> </td> 
   <td colname="2"> 기본 미디어 플레이어 항목 구성 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemLoader.html" format="html" scope="external"> DefaultMediaPlayerItemLoader</a></span> </td> 
   <td colname="2"> 기본 미디어 플레이어 항목 로더입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a></span> </td> 
   <td colname="2">에 대한 공용 인터페이스 <span class="codeph"> DefaultMediaPlayer</span> 클래스. Event, PlayerState 및 Visibility에 대한 열거형을 포함합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerConfig.html" format="html" scope="external"> MediaPlayerConfig</a> </span> </td> 
   <td colname="2"> 미디어 플레이어 구성 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerContext.html" format="html" scope="external"> MediaPlayerContext</a></span> </td> 
   <td colname="2"> 미디어 플레이어에 추가 컨텍스트를 제공하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a></span> </td> 
   <td colname="2"> 오디오-비디오 미디어를 나타내는 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> 기본 미디어 플레이어 항목 구성</a></span> </td> 
   <td colname="2"> 기본 미디어 플레이어 항목 구성 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a></span> </td> 
   <td colname="2">미디어 플레이어 리소스를 로드하고 해당 리소스를 만드는 클래스 <span class="codeph"> MediaPlayerItem</span> 개체. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerStatus.html" format="html" scope="external"> MediaPlayerStatus</a></span> </td> 
   <td colname="2"> 미디어 플레이어의 지원되는 상태를 포함하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a></span> </td> 
   <td colname="2">에서 사용할 보기에 대한 클래스 <span class="codeph"> MediaPlayer</span> 비디오 렌더링용. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> MediaResource</a></span> </td> 
   <td colname="2"> 미디어 리소스에 대한 모든 정보를 래핑하는 클래스입니다. 미디어 리소스 유형에 대한 열거형을 포함합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResourceType.html" format="html" scope="external"> MediaResourceType</a></span> </td> 
   <td colname="2"> 지원되는 미디어 리소스 유형을 포함하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a></span> </td> 
   <td colname="2"> 기본 큐 태그 외에 광고 배치를 수행할 때 미디어 플레이어에서 사용하는 사용자 지정 태그를 캡슐화하는 클래스입니다. 애플리케이션에 알림이 전송되기 원하는 태그 이름도 포함됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> 텍스트 형식</a></span> </td> 
   <td colname="2"> 텍스트 스타일을 설명하는 다른 특성(예: 폐쇄 캡션 스타일)을 캡슐화하는 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> 버전</a></span> </td> 
   <td colname="2"> TVSDK 버전 및 설명을 제공하는 클래스입니다. </td> 
  </tr> 
 </tbody> 
</table>
