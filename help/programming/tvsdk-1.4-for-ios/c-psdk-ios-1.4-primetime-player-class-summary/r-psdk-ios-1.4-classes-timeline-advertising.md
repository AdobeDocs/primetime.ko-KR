---
description: 이러한 클래스는 타임라인 내에서 발생하는 광고에 대한 정보를 제공합니다.
seo-description: 이러한 클래스는 타임라인 내에서 발생하는 광고에 대한 정보를 제공합니다.
seo-title: 타임라인 광고 클래스
title: 타임라인 광고 클래스
uuid: b36d128f-7f13-4c61-b925-dfa5cd94e255
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 타임라인 광고 클래스{#timeline-advertising-classes}

이러한 클래스는 타임라인 내에서 발생하는 광고에 대한 정보를 제공합니다.

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이름 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">광고 추상화를 정의하고 모든 광고 정보를 보유하는 클래스입니다. 고유 ID, 기간 및 MediaResources로 정의됩니다. MediaResource에는 실제 광고 컨텐츠가 있는 URL이 포함되어 있습니다. 
    <ph>
      컨텐츠에 분할된 기본 선형 자산을 나타냅니다. 선형 자산과 함께 표시되어야 하는 동반자 자산의 배열을 선택적으로 포함할 수 있습니다.
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">표시할 자산을 나타내는 클래스입니다. 
    <ph>
      표시할 자산을 나타냅니다.
    </ph> 
    <ph>
      광고 자산을 나타내는 클래스입니다.
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <ph>
      배너 자산을 표시합니다. 응용 프로그램에서 이 유틸리티 클래스의 새 인스턴스를 만들고 배너 에셋을 설정한 다음 뷰에 추가해야 합니다. 배너에 대한 노출 및 클릭 추적은 이 클래스에서 내부적으로 관리합니다.
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">재생하는 동안 특정 시점에 재생되는 여러 광고에 대한 통합 보기를 제공하는 클래스입니다. 
    <ph>
      컨텐츠에 분할된 광고의 연속 시퀀스를 나타냅니다.
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">자산과 연결된 클릭 인스턴스를 나타내는 클래스입니다. 이 인스턴스에는 클릭스루 URL과 사용자에게 추가 정보를 제공하는 데 사용할 수 있는 제목에 대한 정보가 포함되어 있습니다. 
    <ph>
      자산과 연결된 클릭 인스턴스를 나타냅니다. 이 인스턴스에는 클릭스루 URL과 사용자에게 추가 정보를 제공하는 데 사용할 수 있는 제목에 대한 정보가 포함되어 있습니다.
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> AdPolicySelector API 호출에 대한 속성을 정의하는 프로토콜입니다. 이러한 속성은 각 광고 동작을 적용하기 위한 컨텍스트를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PTAdPolicySelector</td> 
   <td colname="2"> 광고 행동을 적용하기 위한 광고 정책 선택기 프로토콜입니다. 애플리케이션은 모든 필수 메서드를 구현하거나 기존 기본 정책 선택기 클래스를 확장하여 특정 비헤이비어를 사용자 정의하여 이 프로토콜을 준수할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> PTAdTimeline</td> 
   <td colname="2"> 컨텐츠 내 브레이크의 타임라인을 나타내는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <ph>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 클래스, <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 프로토콜
    </ph> </td> 
   <td colname="2"> Adobe Primetime 광고 결정 과정에서 광고 해결 부분을 처리하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> 사용자 지정 컨텐츠 해결 프로그램( PTContentResolver <span class="codeph"> )</span> 에서 컨텐츠 해결 상태를 위임자에게 전달하는 데 사용해야 하는 방법을 설명하는 프로토콜입니다. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">배치 정보 요청을 추상화하는 클래스입니다. 해결된 각 광고에는 하나의 배치 정보가 연결되어 있어야 합니다. 배치 정보는 타임라인에서 광고가 배치되는 위치를 설명합니다. 여기에는 다음과 같은 정보가 포함됩니다. 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">배치 위치(ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">배치 유형(프리롤, 미드롤 또는 포스트롤) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">교체할 기본 컨텐츠 청크의 지속 시간 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

