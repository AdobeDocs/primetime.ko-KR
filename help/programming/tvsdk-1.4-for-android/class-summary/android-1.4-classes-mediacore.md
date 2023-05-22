---
description: Primetime 플레이어 API를 사용하여 플레이어의 동작을 사용자 지정할 수 있습니다.
title: Mediacore 클래스
exl-id: fdbe9cd3-a5ca-4935-b9b3-8a6c04aed9ab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Mediacore 클래스 {#mediacore-classes}

Primetime 플레이어 API를 사용하여 플레이어의 동작을 사용자 지정할 수 있습니다.

TVSDK에 대한 전체 API 설명서를 보려면 [Adobe Primetime API 참조](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

이러한 클래스는 미디어 플레이어와 해당 리소스에 대해 설명합니다.
패키지: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>이름 </p> </th> 
   <th colname="2" class="entry"> <p>설명 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> ABRControlParameters</a>  ABRControlParameters</span> </td> 
   <td colname="2"> 모든 적응형 비트 전송률 제어 매개 변수를 캡슐화하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdClientFactory.html" format="html" scope="external"> AdClientFactory</a> </span> </td> 
   <td colname="2"> 영업 기회 감지기를 만들기 위한 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdvertisingFactory.html" format="html" scope="external"> AdvertisingFactory</a> </span> </td> 
   <td colname="2"> 광고 결정 프로세스의 사용자 지정을 허용하는 팩터리 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> 버퍼 제어 매개변수</a> </span> </td> 
   <td colname="2"> 모든 버퍼 제어 매개 변수를 캡슐화하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> 광고 재생 동작에 대한 기본 구현입니다. 애플리케이션에서 광고 동작을 사용자 지정할 수 있는 인터페이스입니다.</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2">의 기본 클래스 구현 <span class="codeph"> MediaPlayer</span> 인터페이스. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a> </span> </td> 
   <td colname="2">에 대한 공용 인터페이스 <span class="codeph"> DefaultMediaPlayer</span> 클래스. Event, PlayerState 및 Visibility에 대한 열거형을 포함합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html" format="html" scope="external"> MediaPlayer.AdPlaybackEventListener</a></span> </td> 
   <td colname="2"> 광고 재생 중에 호출할 콜백 집합의 인터페이스 정의입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html" format="html" scope="external"> MediaPlayer.DRMEventListener</a></span> </td> 
   <td colname="2"> 보호된 메타데이터를 사용할 수 있을 때 호출할 콜백의 인터페이스 정의입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.EventListener.html" format="html" scope="external"> MediaPlayer.EventListener</a> </span> </td> 
   <td colname="2"> 이벤트 리스너 등록을 통합하는 데 사용되는 마커 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html" format="html" scope="external"> MediaPlayer.PlaybackEventListener</a> </span> </td>
   <td colname="2"> 재생 중에 호출할 콜백 집합의 인터페이스 정의입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html" format="html" scope="external"> MediaPlayer.QOSEventListener</a> </span> </td> 
   <td colname="2"> QoS 중에 호출할 콜백 집합의 인터페이스 정의입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a> </span> </td> 
   <td colname="2"> 오디오-비디오 미디어를 나타내는 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a> </span> </td> 
   <td colname="2"> 미디어 플레이어 리소스를 로드하고 해당 MediaPlayerItem 개체를 만드는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html" format="html" scope="external"> MediaPlayerItemLoader.LoaderListener</a> </span> </td> 
   <td colname="2"> MediaPlayerItemLoader 객체와 연관된 리스너 메소드를 정의하는 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a> </span> </td> 
   <td colname="2"> MediaPlayer에서 비디오 렌더링에 사용할 보기용 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> MediaResource</a> </span> </td> 
   <td colname="2"> 미디어 리소스에 대한 모든 정보를 래핑하는 클래스입니다. 미디어 리소스 유형에 대한 열거형을 포함합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PlacementOpportunityDetector.html" format="html" scope="external"> PlacementOpportunityDetector</a> </span> </td> 
   <td colname="2"> 광고 결정 프로세스에 대한 배치로 사용될 매니페스트 내 큐 처리에 사용되는 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a> </span> </td> 
   <td colname="2"> 기본 큐 태그 외에 광고 배치를 수행할 때 미디어 플레이어에서 사용하는 사용자 지정 태그를 캡슐화하는 클래스입니다. 애플리케이션에 알림이 전송되기 원하는 태그 이름도 포함됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> 텍스트 형식</a> </span> </td> 
   <td colname="2"> 텍스트 스타일을 설명하는 다른 특성(예: 폐쇄 캡션 스타일)을 캡슐화하는 인터페이스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormatBuilder.html" format="html" scope="external"> 텍스트 형식 빌더</a></span> </td> 
   <td colname="2"> 텍스트 서식을 설정하는 클래스 메서드입니다. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> 버전</a></span> </td> 
   <td colname="2"> TVSDK 버전 및 설명을 제공하는 클래스입니다. </td> 
  </tr> 
 </tbody> 
</table>
