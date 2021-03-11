---
title: TVSDK 전환 - JavaScript용 1.3에서 2.0
description: 많은 메서드 서명 및 API 요소 이름이 2.0용으로 변경되었습니다. 모든 API 변경 사항을 보려면 이 표를 검토하십시오.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---


# TVSDK 전환 - JavaScript의 경우 1.3에서 2.0{#tvsdk-conversion-to-for-javascript}

많은 메서드 서명 및 API 요소 이름이 2.0용으로 변경되었습니다. 모든 API 변경 사항을 보려면 이 표를 검토하십시오.

## JavaScript {#implement-callback-functions-in-javascript}에서 콜백 함수 구현

메서드 설명서의 주석에서는 구현해야 하는 콜백에 대한 서명을 제안합니다.

JavaScript의 경우 API 구문은 웹 ID를 기반으로 합니다. TVSDK 인터페이스의 경우 메서드 이름을 *methodName*()이라고 합니다. 응용 프로그램에서 구현할 메서드의 경우 *methodName* CallbackFunc라는 읽기/쓰기 특성이 인터페이스에 추가되고 응용 프로그램에서 메서드를 구현하는 함수를 가리키도록 설정해야 합니다. 예:

```shell
// An app implementable interface
interface ContentFactory
{
    /*
     * AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item);
     */
    attribute Object retrieveAdPolicySelectorCallbackFunc;
 
    /*
     * ContentResolverList retrieveResolvers(MediaPlayerItem item);
     */
    attribute Object retrieveResolversCallbackFunc;
 
    /*
     * OpportunityGeneratorList retrieveGenerators(MediaPlayerItem item);
     */
    attribute Object retrieveGeneratorsCallbackFunc;
};

// this is how to implement it
var factory = new AdobePSDK.ContentFactory();
factory.retrieveAdPolicySelectorCallbackFunc = function(item)
{
    // return your adPolicySelector according to the item
    return adPolicySelector;
}
 
mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig ();
playerConfig.adFactory = factory;
// Use this config to load new MediaResource
```

## 2.0 {#advertising-workflow-api-element-changes-for}에 대한 광고 워크플로우 API 요소 변경

다음 표는 버전 1.3과 2.0 간에 JavaScript TV SDK용 광고 워크플로우 API 요소를 비교합니다.

이 항목의 표:

* TimedMetadata
* AdSigningMode
* 광고 메타데이터
* CustomRangeMetadata
* ReplaceTimeRange
* 배치
* 기회
* 예약
* 타임라인/타임라인 항목/타임라인 마커
* AdBreak
* 광고 / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakViewedPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* 타임라인 작업
* AdBreakPlacement
* AuditudeSettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>:interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ; <br /> 부호 없는 짧은 METADATA_TYPE_ID3 = 1 ; <br /> readonly 특성 unsigned short type <br /> readonly 특성 long time;<br /> readonly 특성 DomString id;<br /> readonly 특성 DomString 이름;<br /> readonly 특성 DomString content; <br /> readonly 특성 메타데이터;<br /> }; </p> </td> 
   <td><p>인터페이스 TimedMetadata {<br />은 부호 없는 짧은 METADATA_TYPE_TAG = 0;<br /> 부호 없는 짧은 METADATA_TYPE3 = 1;<br /> 읽기 전용 특성 short metadataType;<br /> 읽기 전용 속성 long id;<br /> 읽기 전용 특성 long id;<br /> 읽기 전용 특성 domString 이름;<br /> <br /> 읽기 전용 특성 메타데이터;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface TimedMetadataList {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter TimedMetadata(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSigningMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdSigningMode { <br /> 는 부호 없는 짧은 MODE_DEFAULT, <br /> 에는 서명되지 않은 짧은 MODE_MANIFEST_CUES, <br /> const unsigned short MODE_SERVER_MAP , <br /> const unsigned short MODE_CUSTOM_RANGES &lt;a/&gt; };<br /></p> </td> 
   <td>MetadataKeys::MANIFEST_CUS 키를 대체합니다.</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMetadata {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdvertisingMetadata { <br /> 속성 AdSigningMode;<br /> 특성 AdBreakViewedPolicy adBreakAsViewed;<br /> 특성 부울 livePreroll;<br /> 특성 부울 delayAdLoading;<br /> };</p> </td> 
   <td>이 기능은<p>메타데이터 키::ADVERTISING_METADATA</p> key.</td> 
  </tr> 
 </tbody> 
</table>

### CustomRangeMetadata {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 CustomRangeMetadata { <br /> 에는 부호 없는 짧은 TYPE_MARK_RANGE;<br />은 부호 없는 짧은 TYPE_DELETE_RANGE;<br />는 부호 없는 짧은 TYPE_REPLACE_RANGE;<br /> 특성 부호 없는 짧은 유형;<br /> 특성 boolean adjustSeekPosition;<br /> 특성 TimeRangeList timeRangeList;<br /> };</p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### ReplaceTimeRange {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ReplaceTimeRange { <br /> 속성 unsigned long begin;<br /> readonly 특성 unsigned long end;<br /> 특성 부호 없는 긴 기간;<br /> 특성 unsigned long replaceDuration;<br /> };</p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 배치 {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 배치 { <br />에 서명되지 않은 짧은 TYPE_MID_ROLL;<br />은 부호 없는 짧은 TYPE_PRE_ROLL;<br />는 부호 없는 짧은 TYPE_POST_ROLL;<br /> 에는 서명되지 않은 짧은 TYPE_SERVER_MAP;<br /> 에는 부호 없는 짧은 TYPE_CUSTOM_RANGE;<br /> 읽기 전용 부호 없는 짧은 유형 특성;<br /> readonly 특성 long time;<br /> readonly 특성 long duration;<br />은 서명되지 않은 짧은 MODE_DEFAULT;<br /> 에는 서명되지 않은 짧은 MODE_INSERT;<br />에 서명되지 않은 짧은 MODE_REPLACE;<br /> 서명되지 않은 짧은 MODE_DELETE;<br />는 부호 없는 짧은 MODE_MARK;<br />에 서명되지 않은 짧은 MODE_FREE_REPLACE;<br /> 읽기 전용 특성 부호 없는 짧은 모드;<br /> 읽기 전용 특성 TimeRange;<br /> };</p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 기회 {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 기회 { <br /> 읽기 전용 특성 DomString id;<br /> 읽기 전용 특성 배치;<br /> 읽기 전용 특성 개체 설정;<br /> 읽기 전용 특성 customParameters;<br /> }; </p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 예약 {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 예약 { <br /> 읽기 전용 특성 TimeRange 범위;<br /> readonly 특성 long hold;<br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 타임라인 / TimelineItem / TimelineMarker {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>타임라인</strong>:인터페이스 타임라인  <br /> { readonly 속성 TimelineMarkerList timelineMarkers; <br /> readonly 특성 TimelineItemList timelineItems; <br /> double convertToLocalTime( double time); <br /> double convertToVirtualTime( double time); <br /> };</p> </td> 
   <td><p>인터페이스 타임라인 {<br /> 읽기 전용 특성 TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>타임라인 항목</strong>:interface TimelineItem: <br /> TimelineMarker {<br /> readonly 특성 long id; <br /> readonly 특성 TimeRange virtualRange; <br /> readonly 특성 TimeRange localRange; <br /> readonly 속성 boolean viewed. <br /> readonly 속성 boolean temporary. <br /> }; </p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><strong>타임라인 마커</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface TimelineMarker {<br /> 읽기 전용 특성 2회;<br /> 읽기 전용 특성 2지속 시간;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdBreak {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreak {<br /> <br /> <br /> 읽기 전용 특성 이중 지속 시간;<br /> 읽기 전용 특성 AdList 광고;<br /> <br /> <br /> 읽기 전용 특성 AdInsertionType 삽입Type;<br /> };<br /> </p> </td> 
   <td><p>interface AdBreak {<br /> 읽기 전용 특성 double time;<br /> 읽기 전용 특성 double replaceDuration;<br /> <br /> 읽기 전용 속성 double duration;<br /> 읽기 전용 속성 AdList adList;<br /> <br /> 읽기 전용 속성 DomString 데이터;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### 광고 / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>광고</strong>:인터페이스 광고 {<br /> readonly 특성 AdAsset primaryAsset;<br /> readonly 특성 AdAssetList companionAssets;<br /> <br /> readonly 속성 double duration;<br /> readonly attribute double duration;readonly attribute DomString id;const short ADTYPE_LINEAR = 0;const <br /> const unsigned short ADTYPE_INLINEAR = 1, <br />  <br /> <br />  <br /> unsigned 속성 짧은 광고 Type;Readonly 특성 AdInsertionType adInsertionType; <br /> <br /> readonly 속성 boolean clickable; <br /> readonly 속성 부울 isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>인터페이스 광고 {<br /> 읽기 전용 특성 AdAsset primaryAsset;<br /> 읽기 전용 특성 AdAssetList companionAssets;<br /> <br /> 읽기 전용 속성 이중 지속 시간;<br /> 읽기 전용 특성 DomString id;<br /> 에는 서명되지 않은 짧은 ADTYPE_LINEAR = 0;<br /> st unsigned short ADTYPE_NANIMAL = 1;<br /> <br /> 읽기 전용 속성 부호 없는 짧은 유형;<br /> 읽기 전용 속성 AdInsertionType insertionType;<br /> 읽기 전용 특성 추적기;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface AdAsset {<br /> 읽기 전용 특성 DomString id;<br /> 읽기 전용 특성 2지속 시간;<br /> 읽기 전용 특성 MediaResource;<br /> 읽기 전용 속성 AdClick adClick;<br /> 읽기 전용 특성 Object 메타데이터;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>인터페이스 AdClick {<br /> 읽기 전용 특성 DomString id;<br /> 읽기 전용 특성 DomString title;<br /> 읽기 전용 특성 DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>광고 목록</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface AdList {<br /> 읽기 전용 특성으로 서명되지 않은 긴 길이;<br /> getter Ad(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface AdAssetList {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter AdAsset(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:interface AdBannerAsset:AdAsset<br /> {<br /> readonly 특성 int width;<br /> readonly 특성 int height;<br /> readonly attribute int height;<br /> readonly attribute DomString staticUrl;<br /> readonly 특성 DomString height;<br /> readonly 특성 DomString width;};</p> </td> 
   <td> 2.0의 새로운 기능</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem / AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>:interface AdBreakTimelineItem:TimelineItem {  <br /> readonly attribute AdBreak adBreak; <br /> readonly 특성 AdTimelineItemList 항목; <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>:interface AdTimelineItem:TimelineItem {  <br /> readonly attribute AdBreak adBreak; <br /> 읽기 전용 속성 광고; <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>:interface AdBreakTimelineItemList {  <br /> readonly 특성 unsigned long length; <br /> getter AdBreakTimelineItem(부호 없는 로그 인덱스); <br /> };</p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakViewedPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPolicy {<br /> 읽기 전용 특성 짧은 AD_BREAK_POLICY_SKIP;<br /> 읽기 전용 속성 짧은 AD_BREAK_POLICY_PLAY;<br /> 읽기 전용 속성 짧은 AD_BREAK_POLICY_REMOVE;<br /> 읽기 전용 특성 짧은 AD_BREAK_BREAK POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> 읽기 전용 특성 짧은 AD_BREAK_POLICY_SKIP;<br /> 읽기 전용 속성 짧은 AD_BREAK_POLICY_PLAY;<br /> 읽기 전용 속성 짧은 AD_BREAK_POLICY_REMOVE;<br /> 읽기 전용 특성 짧은 AD_BREAK_BREAK POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakViewedPolicy {<br /> 읽기 전용 속성 짧은 AD_BREAK_AS_VIEWED_ON_BEGIN;<br /> 읽기 전용 속성 짧은 AD_BREAK_AS_VIEWED_ON_END;<br /> 간단한 AD_BREAK_AS VIEWED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> 읽기 전용 속성 짧은 AD_BREAK_AS_VIEWED_ON_BEGIN;<br /> 읽기 전용 속성 짧은 AD_BREAK_AS_VIEWED_ON_END;<br /> 읽기 전용 속성 짧은 AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> 읽기 전용 특성 짧은 AD_POLICY_PLAY;<br /> 읽기 전용 속성 짧은 AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 읽기 전용 속성 짧은 AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;readonly 속성 short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> 읽기 전용 속성 짧은 AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> 읽기 전용 속성 short AD_POLICY_PLAY;<br /> 읽기 전용 속성 짧은 AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 읽기 전용 속성 짧은 AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> 짧은 AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> 읽기 전용 속성 짧은 AD_POLICY_SKIP_AD_BREAK;<br />..</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> 읽기 전용 특성(짧은 AD_POLICY_MODE_PLAY;<br /> 읽기 전용 특성(짧은 AD_POLICY_MODE_SEEK;<br /> 읽기 전용 속성 짧은 AD_POLICY_MODE_TRICPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> 읽기 전용 속성 짧은 AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> 읽기 전용 특성 AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> 읽기 전용 특성 AdTimelineItem;<br /> 읽기 전용 특성 double currentTime;<br /> 읽기 전용 특성 doubleTo입니다. 시간;<br /> 읽기 전용 특성 이중 속도;<br /> 읽기 전용 속성 짧은 모드;//AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> 읽기 전용 특성 AdBreakPlacementList <br /> adBreakPlacement;<br /> 읽기 전용 속성 Ad 광고;<br /> 읽기 전용 속성 double currentTime;<br /> 읽기 전용 특성 double seekToTime;<br /> 읽기 전용 특성 double rate;<br /> readonly 속성 짧은 모드;//AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 속성 개체 selectPolicyForAdBreakCallback;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 속성 개체 selectAdBreaksToPlayCallback; <br /> /**<br /> * AdPolicy selectForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 속성 개체 selectPolicyForSeekIntoAdCallbackFunc;<br /> /**<br /> * AdBreakViewedPolicy selectViewedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 selectViewedObjectedPolicy policyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>인터페이스 AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForAdBreakCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 속성 개체 selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 속성 개체 selectPolicyForSeekIntoAdCallback;<br /> /**<br /> * AdBreakAsViewed selectViewedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 selectViewedObservedInfo policyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimelineOperation {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface TimelineOperation { <br /> 읽기 전용 특성 배치<br /> };</p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPlacement {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPlacement :TimelineOperation {<br /> 읽기 전용 특성 AdBreak adBreak;<br /> 읽기 전용 특성 배치;// From TimelineOperation<br /> readonly 특성 double time;<br /> readonly 특성 double duration;<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> 읽기 전용 특성 AdBreak adBreak;<br /> 읽기 전용 속성 배치;<br /> 읽기 전용 속성 두 시간;<br /> 읽기 전용 속성 이중 지속 시간;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AuditudeSettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AuditudeSettings :AdvertisingMetadata { <br /> 속성 DomString zoneId;<br /> 특성 DomString mediaId;<br /> 특성 DomString defaultMediaId;<br /> 특성 DomString 도메인;<br /> 특성 Object targettingInfo;<br /> 특성 customParameters;<br /> 특성 Boolean creativePackingEnabled;<br /> 특성 Boolean showStaticBanners;<br /> };</p> </td> 
   <td>기능은 MetadataKeys::AUDITUDE_METADATA_KEY 키에 의해 제공되었습니다.</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#customization-api-element-changes-for}에 대한 사용자 정의 API 요소 변경

다음 표는 버전 1.3과 2.0 간에 JavaScript TV SDK에 대한 사용자 정의 API 요소를 비교합니다.

이 항목의 표:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemConfig {<br /> 특성 ContentFactory adFactory;<br /> 특성 StringList subscribeTags;<br /> <br /> 속성 StringList adTags;<br /> <br /> 속성 AdSigningMode adSigningMode;<br /> 특성 CustomRangeMetadata customRangeMetadata;<br /> 특성 NetworkConfiguration networkConfiguration;<br /> 특성 AdvertisingMetadata advertisingMetadata;<br /> 특성 Boolean useHardwareDecoder;<br /> };<br /></p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /> <br /> 속성 StringList adTags;<br /> 속성 StringList subscribedTags;<br /> 속성 MediaPlayerClientFactory Factory;<br /> <br /> <br /> <br /> a10/&gt; <br /> };<br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem 항목);<br /> */<br /> 속성 객체 retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem 항목);<br /> */<br /> 속성 개체 검색AdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> 속성 boolean forceNativeNetworking;<br /> 속성 boolean useRedirectedUrl;<br /> 속성 Object cookieHeader;<br /> 속성 boolean readSetCookieHeader;<br /> 특성 int masterUpdateInterval;<br /> 특성 부울 useCookieHeaderForAllRequests;<br /> 특성 int readLimit;<br /> };</p> </td> 
   <td>1.3에서는 이 기능 중 일부가 MetadataKeys에서 제공되었습니다</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#drm-api-element-changes-for}에 대한 DRM API 요소 변경

다음 표는 버전 1.3과 2.0 간에 JavaScript TVSDK에 대한 DRM API 요소를 비교합니다.

이 항목의 표:

* DRM 워크플로우 초기화
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### DRM 워크플로 초기화 {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>DRM 워크플로우를 시작하려면 응용 프로그램에서 AdobePSDK.initiateDRMWorkflow를 호출해야 합니다. 이 호출이 없으면 DRM 비디오가 재생되지 않습니다.<p>인터페이스 AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> 부울 privacyModeOn);<br /> };</p> </td> 
   <td>초기화가 내부적으로 완료되었으며 명시적 호출이 필요하지 않았습니다.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0에는 변경 사항이 없습니다. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| 2.0에는 변경 사항이 없습니다. | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### 메타데이터 {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에는 변경 사항이 없습니다.</td> 
   <td><p>인터페이스 DRMMetadata<br /> {<br /> 읽기 전용 특성 DomString serverUrl;<br /> 읽기 전용 특성 DomString licenseId;<br /> 읽기 전용 특성 DRMPolicyArray 정책;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly 특성 int playbackPeriodInSeconds;<br /> readonly 특성 long playbackStartDate;<br /> readonly 특성 long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly 특성 int periodInSeconds;<br /> readonly 특성 int startDate;<br /> readonly 특성 int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에는 변경 사항이 없습니다.</td> 
   <td><p>인터페이스 DRMLicense {<br /> 읽기 전용 특성 Uint8Array 바이트;<br /> 읽기 전용 속성 Date licenseStartDate;<br /> 읽기 전용 속성 Date licenseEndDate;<br /> 읽기 전용 속성 Date offlineStorageDate;<br /> 읽기 전용 특성 DateStorageEndAttribute 날짜;<br /> 읽기 전용 특성 DomString serverUrl;<br /> 읽기 전용 특성 DomString licenseID;<br /> 읽기 전용 특성 DomString policyID;<br /> 읽기 전용 특성 DRMPlaybackTimeWindow playbackTimeWindow;<br /> 읽기 전용 특성 ObjectProperties; <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMLicenseDomain {<br /> readonly 특성 DomString authenticationDomain;<br /> readonly 특성 DRMAuthenticationMethod authenticationMethod;<br /> readonly 특성 DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> 읽기 전용 특성 DomString authDomain;<br /> 읽기 전용 특성 DRMAuthenticationMethod authMethod;<br /> 읽기 전용 특성 DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 DRMPolicy<br /> {<br /> 읽기 전용 특성 DomString authenticationDomain;<br /> 읽기 전용 특성 DRMAuthenticationMethod authenticationMethod;<br /> <br /> 읽기 전용 특성 DomString displayName;<br /> 읽기 전용 특성 DRMLicenseDomain 도메인;<br /> };</p> </td> 
   <td><p>인터페이스 DRMPolicy<br /> {<br /> 읽기 전용 특성 DomString authDomain;<br /> 읽기 전용 특성 DRMAuthenticationMethod authMethod authMethod authMethod;<br /> 읽기 전용 특성 DomString dispName;<br /> 읽기 전용 특성 DRMLicenseDomain licenseDomain; a5/&gt; };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 관리자:EventTarget {<br /> void acquireLicense(DRMMetadata 메타데이터 메타데이터, <br /> DRMAcquireLicenseSettings 설정, <br /> DRMAquireLicenseListener);<br /> void acquirePreviewLicense(DRMMetadata, <br /> DRMAb QuireLicenseListener);<br /> void authenticate(DRMMetadata, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString 사용자, <br /> DomString 암호, <br /> DRMAuthenticate리스너);<br /> <br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array, DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br /> 속성 long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener);&lt;a 21/&gt; void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /> <br /> voidDRMO perationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> boolean commitImmediate,<br /> DRMReturn수신기 );<br /> void setAuthenticationToken(<br /> DRMMetadata 메타데이터, <br /> DomString authenticationDomain, <br /> Uint8Array 토큰, <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>인터페이스 관리자:EventTarget {<br /> void acquireLicense(DRMMetadata 메타데이터, <br /> DRMAcquireLicenseSettings 설정, <br /> EventContext eventContext);<br /> void acquirePreviewLicense(DRMMetadata, <br /> EventContext 컨텍스트 컨텍스트 컨텍스트 컨텍스트 컨텍스트 );<br /> void authenticate(DRMMetadata 메타데이터, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString 사용자, <br /> DomString 암호, <br /> EventContext);<br /> 12/&gt; DRMMetadata createMetadataFromBytes(<br /> Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> 속성 long maxOperationTime;<br /> a17/&gt; void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> voidLicenseDomain(<br /> DRML LicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> Dom 문자열 licenseID,<br /> DomString policyID, <br /> boolean commitImmediate,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> DRMMetadata, &lt;a333 3/&gt; DomString authenticationDomain, <br /> Uint8Array 토큰, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext);&lt;a333 8/&gt; };<br /><br /><br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMErrorListener :<br /> 공용 psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkls:PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protected:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>DRMManger의 비동기 메서드 중 하나에 오류가 발생하면</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMOperationCompleteListener :<br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete() = 0;<br /> <br /> protected:<br /> 가상 ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMIintializationComplete<p>/ PSDKEvent</p> <p>DRM의 초기화가 완료되면</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>joinLicenseDomain() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>leaveLicenseDomain() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>resetDRM() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>setAuthenticationTokenSet() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>storeLicenseBytes() 작업이 성공적으로 완료되면</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMAuthenticateListener :<br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> 가상 DRAG maUthenticateListener() {}<br /> }<br /></p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>DRMManager::authenticate 메서드 호출이 성공한 경우</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMAquireLicenseListener:<br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAcquisition(const DRMLicense*) = 0;<br /> <br /> protected:<br /> virtual ~DRMAquireLicenseListener()} { a6/&gt; };<br /></p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquisted<p>/ DRMLicenseImportedEvent</p> <p>DRMManager::acquirePreviewLicense 메서드 호출이 성공한 경우</p> </li> 
     <li>kEventDRMLicenseAccessed<p>/ DRMLicenseImportedEvent</p> <p>DRMManager::acquireLicense 메서드 호출이 성공한 경우</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>클래스 DRMReturnLicenseListener:<br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned) = 0;<br /> <br /> protected:<br /> virtual ~DRMReturnLicenseListener() {} };<br /></p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>DRMManager::returnLicense 메서드 호출이 성공한 경우</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#generic-playback-api-element-changes-for}에 대한 일반 재생 API 요소 변경

다음 표는 JavaScript TVSDK 1.3과 2.0 간의 일반 재생 API 요소를 비교합니다.

이 항목의 표:

* MediaResource
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> 속성 DomString url;<br /> 특성 부호 없는 짧은 유형;<br /> 특성 개체 메타데이터;<br /> 부호 없는 짧은 TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> 특성 DomString url;<br /> 특성 DomString 유형;<br /> 속성 개체 메타데이터;<br /> <br /> <br /> <br /> <br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 MediaPlayer :EventTarget<br /> {<br /> void prepareToPlay( 이중 위치);<br /> void play();<br /> void pause();<br /> void seek( 이중 위치);<br /> void seekToLocal( 이중 위치);<br /> void release(); a8/&gt; void replaceCurrentItem(MediaPlayerItem);<br /> void replaceCurrentResource(MediaResource rsource, <br /> MediaPlayerItemConfig);<br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> <br /> 읽기 전용 속성 TimeRange playbackRange;<br /> 읽기 전용 특성 TimeRange;<br /> readonly 특성 double currentTime;<br /> readonly 특성 double localTime;<br /> readonly 특성 TimeRange bufferedRange;<br /> readonly 특성 DRMManagerManager;<br /> readonly 특성 MediaPlayerCurrentItem;&lt;a22 <br /> <br /> // PlayerStatus<br /> <br /> <br /> 서명되지 않은 짧은 PLAYER_STATUS_INITIALIZED;<br /> 서명되지 않은 짧은 PLAYER_STATUS_PREPARING;<br /> 서명되지 않은 짧은 PLAYER_PREPARINGstatus_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> 서명되지 않은 짧은 PLAYER_STATUS_조회수;&lt;A32/&gt; 서명되지 않은 짧은 PLAYER_STATUS_STATUS complete;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> 읽기 전용 부호 없는 짧은 상태 특성;<br /> <br /> 속성 짧은 볼륨;&lt;a33 9/&gt; 특성 ABRControlParameters abrControlParameters;<br /> 특성 BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE;//CC 가시성<br /> 에는 부호 없는 짧은 INVISIBLE;//CC 가시성<br /> 특성 부호 없는 짧은 Visibility;<br /> 특성 TextFormat ccStyle;<br /> 읽기 전용 특성 PlaybackMetrics playbackMetrics;<br /> <br /> 속성 이중 속도;<br /> 특성 MediaPlayerStyleStyle 보기 보기;<br /> 읽기 전용 특성 타임라인;<br /> 특성 double currentTimeUpdateInterval;<br /> // 이 설정은 2.0<br /> };에서 지원되지 않습니다.<br /><br /><br /><br /></p> </td> 
   <td><p>인터페이스 MediaPlayer :EventTarget<br /> {<br /> void prepareToPlay( int position);<br /> void play();<br /> void pause();<br /> void seek( int position);<br /> void seekToLocalTime( int position);<br /> void release( );<br /> void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> 읽기 전용 특성 TimeRange playbackRange;<br /> 읽기 전용 attribute TimeRange seekableRange;<br /> readonly 특성 double currentTime;<br /> readonly 특성 double localTime;<br /> readonly 특성 TimeRange bufferedRange;<br /> 읽기 전용 특성 DRMManagerManager;<br /> MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> 에는 서명되지 않은 짧은 PLAYER_STATE_IDLE;<br /> 서명되지 않은 짧은 PLAYER_STATE_INITIALIZING;<br />에는 서명되지 않은 짧은 PLAYER만 있습니다. STATE_INITIALIZED;<br />은(는) 서명되지 않은 짧은 PLAYER_STATE_PREPARING;<br />은(는) 서명되지 않은 짧은 PLAYER_STATE_PREPARING;<br />은 서명되지 않은 짧은 PLAYER_STATE PAUSED;<br /> 부호 없는 짧은 PLAYER_STATE_MODERING;<br /> 부호 없는 짧은 PLAYER_STATE_COMPLETE;<br /> 부호 없는 짧은 PLAYER_STATE_ERROR;<br /> 부호 없는 짧은 PLAYER_STATE_RELEASED;<br /> 에는 부호 없는 짧은 PLAYER_STATUS_SUSPENDED;<br /> 읽기 전용 부호 없는 짧은 상태;<br /> <br /> 특성 부호 없는 짧은 볼륨;<br /> 특성 ABRControlParameters abrControlParameters;<br /> 특성 BufferControlParameters bufferControlParameters;<br /> <br /> 읽기 전용 서명되지 않은 짧은 VISIBLE;//CC 가시성<br /> 읽기 전용 부호 없는 짧은 INVISIBLE;//CC 가시성<br /> 특성 부호 없는 짧은 Visibility;<br /> 특성 TextFormat ccStyle;<br /> 읽기 전용 특성 PlaybackMetrics playbackMetrics;<br /> 특성 MediaPlayerConfig;<br /> 특성 이중 속도;<br /> 특성 MediaPlayerView;<br /> 읽기 전용 특성 타임라인;<br /> <br /> <br /> };<br /><br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br />은(는) 서명되지 않은 짧은 PLAYER_STATUS_IDLE;<br /> 서명되지 않은 짧은 PLAYER_STATUS_INITIALIZING;<br />에는 서명되지 않은 짧은 PLAYER_STATUS_INITIALIZED;<br /> player_STATUS_PREPARING;<br /> 서명되지 않은 짧은 PLAYER_STATUS_PREPARED;<br /> 서명되지 않은 짧은 PLAYER_STATUS_PLAYING;<br /> 짧은 PLAYER_STATUS_PAUSED;<br /> 서명되지 않은 짧은 PLAYER_STATUS_LOOKING;&lt;a1111 0/&gt; 서명되지 않은 짧은 PLAYER_STATUS_COMPLETE;<br />에 서명되지 않은 짧은 PLAYER_STATUS_ERROR;<br /> 서명되지 않은 짧은 PLAYER_STATUS_RELEASED;<br />에는 서명되지 않은 짧은 PLAYER_STATUS_SUSPENDED;<br /> };<br /></p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

#### MediaPlayer {#events-supported-by-mediaplayer}에서 지원하는 이벤트

<table> 
 <tbody> 
  <tr> 
   <th>2.0 이벤트 이름</th> 
   <th>2.0 인터페이스</th> 
   <th> </th> 
   <th>1.3 이벤트 이름</th> 
   <th>1.3 인터페이스</th> 
  </tr> 
  <tr> 
   <td><p>(2.0에 대해 삭제됨)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>준비된 문서</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>미디어 플레이어 항목이 업데이트될 때.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>updated</p> <p>미디어 플레이어가 미디어를 성공적으로 업데이트한 경우</p> </td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TtmedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdated</td> 
   <td>이벤트</td> 
   <td> </td> 
   <td>타임라인 업데이트됨</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>2.0에서 삭제됨</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>2.0에 대해 삭제됨</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>stateChanged</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>SizeEvent</td> 
   <td> </td> 
   <td>크기</td> 
   <td>SizeEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adStarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adStart</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>adCompleted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>timeChanged</td> 
   <td>TimeEvent</td> 
   <td> </td> 
   <td>진행률</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>이벤트</td> 
   <td> </td> 
   <td>버퍼</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>이벤트</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>TimeEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>NotificationEvent</td> 
   <td> </td> 
   <td>operationFailed</td> 
   <td>ErrorEvent</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reservationReached</td> 
   <td>ReservationEvent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TimelineHolderEvent</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakSwedger</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSwedger</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClicked<br /> 사용자가 광고를 클릭할 때</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> 재생 프로필이 변경될 때.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdminated<br /> 내부 또는 외부 규칙으로 인해 검색 위치가 조정되는 경우</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> 미디어 플레이어 항목이 업데이트될 때 재생 시간에만 검색할 수 있는 오디오 트랙이 포함된 특정 스트림의 경우 이 이벤트는 새 오디오 트랙을 사용할 수 있을 때 발생합니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captions미디어 플레이어 항목이 업데이트될 때 <br /> 업데이트 실시간/선형 스트림의 경우 클라이언트는 미디어 리소스를 정기적으로 새로 고쳐서 사용 가능한 새로운 컨텐츠를 감지해야 합니다. 이러한 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> 미디어 플레이어 항목이 업데이트되면 실시간/선형 스트림의 경우 클라이언트는 미디어 리소스를 정기적으로 새로 고쳐서 사용 가능한 새로운 컨텐츠를 감지해야 합니다. 이러한 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> 미디어 플레이어 항목이 업데이트될 때 실시간/선형 스트림의 경우 클라이언트는 미디어 리소스를 정기적으로 새로 고쳐서 사용 가능한 새로운 컨텐츠를 감지해야 합니다. 이러한 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> 시간 지정 이벤트가 생성될 때 전송됩니다.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ABRControlParameters<br /> {<br /> 에서는 서명되지 않은 짧은 ABR_POLICY_REVOR = 0;<br /> 서명되지 않은 짧은 ABR_POLICY_MODERATE = 1;<br />에는 서명되지 않은 짧은 ABR_POLICY_OBG = 2, <br /> <br />&gt; 특성 부호 없는 짧은 abrPolicy;<br /> 특성 부호 없는 int initialBitRate;<br /> 특성 부호 없는 int minBitRate;<br /> 특성 부호 없는 int maxBitRate;<br /> 부호 없는 짧은 DEFAULT_ABR_INITIAL_BITRATE;<br /> 부호 없는 짧은 DEFAULT DEFAULT_ABR_MIN_BITRATE;<br /> 부호 없는 짧은 DEFAULT_ABR_MAX_BITRATE;<br /> ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> 에서는 서명되지 않은 짧은 ABR_POLICY_REVOR = 0;<br /> 서명되지 않은 짧은 ABR_POLICY_MODERATE = 1;<br />에는 서명되지 않은 짧은 ABR_POLICY_OBG = 2, <br /> <br />&gt; 특성 부호 없는 짧은 abrPolicy;<br /> 특성 부호 없는 int initialBitRate;<br /> 특성 부호 없는 int minBitRate;<br /> 특성 부호 없는 int maxBitRate;<br /> <br /> <br /> <br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface BufferControlParameters<br /> {<br /> 특성 이중 initialBufferTime;<br /> 속성 double playBufferTime;<br /> const double double DEFAULT_INITIAL_BUFFER_TIME;<br />에는 이중 DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> 특성 이중 initialBufferTime;<br /> 속성 double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 없음</td> 
   <td><p>interface TextFormat<br /> {<br /> // Color<br />은 부호 없는 짧은 COLOR_DEFAULT = 0;<br />은 부호 없는 짧은 COLOR_BLACK = 1;<br />은 부호 없는 짧은 COLOR_GRAY = 2;<br /> 부호 없는 짧은 COLOR_WHITE = 3;/&gt; 부호 없는 짧은 짧은 COLOR_BRIGHT_WHITE = 4;<br /> 부호 없는 짧은 COLOR_DARK_RED = 5;<br /> 부호 없는 짧은 COLOR_RED = 6;<br /> 부호 없는 짧은 COLOR_BRIGHT_RED = 7;<br /> 부호 없는 짧은 색상_DARK_GREEN = 8;<br /> 부호 없는 짧은 COLOR_GREEN = 9;<br /> 부호 없는 짧은 COLOR_BRIGHT_GREEN = 10;<br /> 부호 없는 짧은 COLOR_DARK_BLUE = 11;<br /> const short COLOR_BLUE = 12;<br /> 부호 없는 짧은 COLOR_BRIGHT_BLUE = 13;<br /> 부호 없는 짧은 COLOR_DARK_YELLOW = 14;<br /> 부호 없는 짧은 COLOR_YELLOW = 15;<br /> 부호 없는 짧은 짧은 COLOR_BRIGHT_YELLOW = 16;<br />은 부호 없는 짧은 짧은 COLOR_DARK_MAGENTA = 17;<br />은 짧은 COLOR_MAGENTA = 18;<br /> 짧은 COLOR_BRIGHT_MAGENTA = 19 ;<br />은 부호 없는 짧은 COLOR_DARK_CYAN = 20;<br />은 부호 없는 짧은 COLOR_CYAN = 21;<br /> 부호 없는 짧은 COLOR_BRIGHT_CYAN = 22;<br /> <br /> readonly 특성 unsigned short fontColor;<br /> readonly 특성 unsigned short backgroundColor;<br /> readonly attribute unsigned short fillColor;<br /> readonly 특성 unsigned short edgeColor;<br /> <br /> //&gt; Size<br /> unsigned 짧은 SIZE SIZE 기본값 = 0;<br />은 부호 없는 짧은 SIZE_SMALL = 1;<br /> const signed short SIZE_MEDIUM = 2;<br /> const short SIZE_LARGE = 3; a36/&gt; <br /> 읽기 전용 속성 짧은 크기;&lt;a33 8/&gt; <br /> // FontEdge<br />은 부호 없는 짧은 FONT_EDGE_DEFAULT = 0;<br /> 부호 없는 짧은 FONT_EDGE_NONE = 1;<br /> 에는 서명되지 않은 짧은 짧은 FONT_EDGE_RAISE = 2;&lt;a4 3/&gt;은(는) 부호 없는 짧은 FONT_EDGE_DUMULED = 3,<br /> 부호 없는 짧은 짧은 FONT_EDGE_UNIFORM = 4,<br /> 부호 없는 짧은 짧은 FONT_EDGE_DROP_SHADOW_LEFT = 5,<br /> 부호 없는 짧은 FONT_EDGE DROP_SHADOW_RIGHT = 6;<br /> 읽기 전용 특성 unsigned short fontEdge;<br /> <br /> // Font<br /> 부호 없는 짧은 FONT_DEFAULT = 0;<br /> 부호 없는 짧은 FONT_MONSPACED_SERIFS = 1;<br />은 부호 없는 짧은 FONT_PROPORTIONAL_WITH_SERIFS = 2;<br /> 부호 없는 짧은 FONT_MONSPACED_WITHOUT_SERIFS = 3;<br /> 부호 없는 짧은 FONT_CANCALE = 4;<br /> 부호 없는 짧은 짧은 FONT_CURSPECTIVE = 5;<br /> const unsigned short FONT_SMALL_CAPTURES = 6;<br /> 읽기 전용 부호 없는 짧은 글꼴;<br /> 읽기 전용 특성 unsigned short fontOpacity;<br /> 읽기 전용 특성 unsigned short backgroundOpacity;<br />&gt; 읽기 전용 특성 unsigned short fillOpacity;<br /> 읽기 전용 속성 unsigned short DEFAULT_OPACITY;<br /> };<br /><br /><br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource, long resourceId,<br /> ItemLoaderListener, <br /> MediaPlayerItemConfig);<br /> void();<br /> 읽기 전용 특성 MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#media-characteristics-api-element-changes-for}에 대한 미디어 특성 API 요소 변경

다음 표는 버전 1.3과 2.0 간에 C++ TVSDK에 대한 미디어 특성 API 요소를 비교합니다.

이 항목의 표:

* MediaPlayerItem
* Track, AudioTrack, ClosedCaptionsTrack
* 프로필
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {<br /> 읽기 전용 특성 MediaResource;<br /> readonly 특성 long resourceId;<br /> readonly 속성 boolean live;<br /> <br /> 읽기 전용 속성 boolean hasAlternateAudio;<br /> 읽기 전용 특성 AudioList audioTracks;<br /> 읽기 전용 attribute AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack);<br /> <br /> 읽기 전용 특성 boolean hasClosedCaptions;<br /> 읽기 전용 특성 ClosedCaptionsTrackClosedCaptionsTracks;<br /> 읽기 전용 특성 ClosedCaptionsTrack selectedTracks;<br /> voidClosedCaptionsTrack track(<br /> ClosedCaptionsTrack 트랙);<br /> <br /> 읽기 전용 특성 boolean hasTimedMetadata;<br /> readonly 특성 TimedMetadataList timedMetadata;<br /> 읽기 전용 특성 boolean;<br /> <br /> 읽기 전용 속성 boolean isProtected;<br /> 특성 DRMMetadataInfoList drmMetadataInfos;<br /> 읽기 전용 특성 ProfileList 프로필;<br /> 읽기 전용 특성 SelectedProfile;<br /> 읽기 전용 특성 BooleanPlaySupported;<br /> 읽기 전용 특성 floatArray availablePlaybackRate;<br /> readonly 특성 float selectedPlaybackRate;<br /> <br /> <br /> 읽기 전용 특성 MediaPlayer mediaPlayer;<br /> 읽기 전용 특성 MediaPlayerItemConfig;<br />&gt; };<br /></p> </td> 
   <td><p>interface MediaPlayerItem {<br /> 읽기 전용 특성 MediaResource;<br /> readonly 특성 long resourceId;<br /> readonly 속성 boolean live;<br /> <br /> 읽기 전용 속성 boolean hasAlternateAudio;<br /> 읽기 전용 특성 AudioList audioTracks;<br /> 특성 audioTrack selectedAudioTrack;<br /> <br /> 읽기 전용 특성 boolean hasClosedCaptions;<br /> 읽기 전용 특성 ClosedCaptionsTrackList ccTracks;<br /> 특성 ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> 읽기 전용 특성 boolean hasTimedMetadata;<br /> 읽기 전용 특성 TimedMetadataList Metadata;<br /> 읽기 전용 특성 부울,<br /> 읽기 전용 특성은 protected; a20/&gt; 읽기 전용 특성 DRMMetadataInfoList drmMetadataInfos;<br /> 읽기 전용 특성 ProfileList 프로필;<br /> <br /> <br /> 읽기 전용 특성 trickPlaySupported;<br /> 읽기 전용 특성 IntIntInfo 32Array availablePlaybackRate;<br /> <br /> 읽기 전용 특성 StringList adTags;<br /> <br /> 읽기 전용 특성 MediaPlayer;<br /> <br /> };<br /><br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### 트랙 / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 추적<br /> {<br /> 읽기 전용 특성 DomString 이름;<br /> 읽기 전용 특성 DomString 언어;<br /> 읽기 전용 속성 boolean default;<br /> 읽기 전용 특성 autoSelect;<br /> }; </p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack :트랙<br /> {<br /> 읽기 전용 특성 DomString name;//FromTrack<br /> 읽기 전용 특성 DomString 언어;//FromTrack<br /> 읽기 전용 특성 부울 기본값;// Track<br /> 읽기 전용 특성 부울 autoSelect;//FromTrack<br /> <br /> 읽기 전용 특성 unsigned int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> 읽기 전용 특성 DomString 이름;<br /> 읽기 전용 특성 DomString 언어;<br /> readonly 특성 boolean default;<br /> readonly 특성 boolean autoSelect;<br /> readonly 특성 boolean forced;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 없음</td> 
   <td><p>interface AudioTrackList<br /> {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter AudioTrack(부호 없는 긴 인덱스);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack :트랙<br /> {<br /> 읽기 전용 특성 DomString name;//FromTrack<br /> 읽기 전용 특성 DomString 언어;//FromTrack<br /> 읽기 전용 특성 부울 기본값;/// FromTrack<br /> 읽기 전용 특성 boolean autoSelect;//FromTrack<br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> 부호 없는 짧은 SERVICE_708_CAPTIONS = 1;<br /> 부호 없는 짧은 SERVICE_WEB_VTT_CAPTIONS = 2;<br /> 읽기 전용 특성 unsigned short serviceType;<br /> readonly 특성 boolean forced;<br /> };<br /></p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> 읽기 전용 특성 DomString 이름;<br /> 읽기 전용 특성 DomString 언어;<br /> 읽기 전용 속성 부울 기본값;<br /> <br /> <br /> 읽기 전용 속성 부울 활성;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 없음</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter ClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 프로필 {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>프로필:2.0에 대한 변경 없음</td> 
   <td><p>인터페이스 프로필<br /> {<br /> 읽기 전용 특성 부호 없는 int width;<br /> 읽기 전용 특성 부호 없는 int height;<br /> 읽기 전용 특성 unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>프로필 목록:2.0에 대한 변경 없음</td> 
   <td><p>interface ProfileList<br /> {<br /> 읽기 전용 특성인 긴 길이;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>:2.0에 대한 변경 없음</td> 
   <td><p>interface DRMMetadataInfo<br /> { <br /> 읽기 전용 특성 DRMMetadata 메타데이터;<br /> readonly 특성 long prefetchTimestamp;<br /> 읽기 전용 특성 TimeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0에 대한 변경 없음</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> 읽기 전용 특성 미등록 긴 길이;<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 다른 언어의 C++ 오류에 대한 예외 매핑 {#mapping-c-errors-to-exceptions-in-different-languages}

C++ 오류 코드를 다른 언어로 된 예외에 매핑할 수 있습니다.

C++ PSDK에는 API에 대한 &quot;throw 없음&quot; 정책이 있습니다. 대부분의 API 메서드는 메서드가 성공적으로 실행되었는지 여부를 나타내기 위해 PSDKErrorCode 값을 반환합니다. 비동기 오류는 오류 이벤트를 통해 알립니다.

ActionScript 및 JAVA SDK의 정책은 다릅니다. 대부분의 오류는 메서드의 동기 부분을 실행할 수 없음을 나타내기 위해 ArgumentError 또는 IllegalStateException을 throw합니다. 이러한 예외는 catch되지 않으며 응용 프로그램 코드는 예외를 처리해야 합니다. 일반적으로 메서드 호출이 실패한 이유에 대한 유용한 정보를 전달합니다. 예를 들어 prepareToPlay 명령이 잘못된 상태에서 호출되면 다음 예외가 발생합니다.

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

또한 ActionScript/JAVA는 일부 내부 객체가 잘못 생성되었음을 나타내는 생성자의 예외를 throw합니다. 이러한 예외는 내부적으로 처리되며 응용 프로그램에 전파되지 않습니다. 예외 사항은 응용 프로그램에 전송되는 경고 알림에 포함됩니다

예를 들어 수신된 광고 응답에 대해 유효한 미디어 파일을 찾을 수 없으면 유효한 광고 자산 개체 또는 광고를 만들 수 없습니다. 따라서 타임라인에 광고가 배치되지 않고 NotificationEvent.OperationFailed 알림이 전달됩니다.

Adobe 비디오 엔진(AVE)에서 비동기식으로 수신되는 오류 또는 경고 코드는 일반 이벤트로 응용 프로그램에 전달됩니다. 알림 이벤트에는 수신된 모든 오류 코드와 URL, 리소스 식별자, 핸들 등과 같은 추가 메타데이터가 포함되어 있습니다. 오류가 심각하고 현재 미디어를 계속 재생할 수 없는 경우 MediaPlayer는 ERROR 상태로 전환되고 onStatusChanged 콜백 또는 MediaPlayerStatusChanged.STATUS_CHANGED 이벤트가 전달됩니다. 재생을 계속할 수 있는 경우 일반 알림 이벤트가 전달됩니다.

<table> 
 <tbody> 
  <tr> 
   <th>C++ 오류(PSDKError 코드)</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>코드 = 1, description = "INVALID_ARGUMENT" 및 additionalInfo= &lt;이 예외를 throw한 메서드에 의해 전달된 값&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>코드 = 2, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 throw한 메서드에 의해 전달된 값&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>코드 = 3, description = "ILLEGAL_STATE" 및 additionalInfo= &lt;이 예외를 throw한 메서드에 의해 전달된 값&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 4, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 throw한 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>코드 = 5, description = "CREATION_FAILED" 및 additionalInfo= &lt;이 예외를 throw한 메서드에 의해 전달된 값&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>코드 = 5, description = "CREATION_FAILED" 및 additionalInfo= &lt;이 예외를 throw한 메서드에 의해 전달된 값&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 7, description = "DATA_NOT_AVAILABLE" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 8, description = "SEEK_ERROR" 및 additionalInfo= &lt;이 예외를 throw한 메서드에서 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 9, description = "UNSUPPORTED_FEATURE" 및 additionalInfo= &lt;이 예외를 throw한 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 10, description = "RANGE_ERROR" 및 이 예외를 throw한 메서드에 의해 전달된 경우)</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 11), description = "CODEC_NOT_SUPPORTED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 12), description = "MEDIA_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 13), description = "NETWORK_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error 또는 MediaPlayerNotification.Warning</td> 
   <td>MediaError 또는 NotificationEvent</td> 
   <td>예외(코드 = 14), description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 throw한 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 15), description = "INVALID_SEEK_TIME" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>코드 = 16, description = "AUDIO_TRACK_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAaccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 17), description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 throw한 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 18), description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 throw한 메서드에 의해 전달됨)</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 19), description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 throw한 메서드에서 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 200, description = "PLAYBACK_OPERATION_FAILED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>코드 = 201, description = "NATIVE_WARNING" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>코드 = 202, description = "AD_RESOLVER_FAILED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에서 전달됨&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#utility-and-helper-api-element-changes-for}에 대한 유틸리티 및 도우미 API 요소 변경 사항

다음 표에서는 버전 1.3과 2.0 간에 JavaScript TVSDK에 대한 유틸리티 및 도움말 API 요소를 비교합니다.

이 항목의 표:

* 버전
* 시간 범위
* QOSProvider
* 장치 정보
* LoadInfo
* 보기
* 재생 정보

### 버전 {#version}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 버전<br /> {<br /> 읽기 전용 특성 DomString 버전;<br /> 읽기 전용 특성 DomString 설명;<br /> 읽기 전용 특성 long major;<br /> 읽기 전용 속성 long minor;<br /> 읽기 전용 특성 long apiVersion;<br /> };<br /></p> </td> 
   <td><p>인터페이스 버전<br /> {<br /> 읽기 전용 특성 DomString 버전;<br /> 읽기 전용 특성 DomString 설명;<br /> 읽기 전용 특성 DomString 주;<br /> 읽기 전용 속성 DomString 부;<br /> 읽기 전용 특성 DomString 개정;<br /> 읽기 전용 특성 DomStringApi version;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 시간 범위 {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 없음</td> 
   <td><p>interface TimeRange<br /> {<br /> 읽기 전용 특성 unsigned long begin;<br /> 읽기 전용 특성 unsigned long end;<br /> readonly 특성 unsigned long duration;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 없음</td> 
   <td><p>인터페이스 QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer);<br /> void detachMediaPlayer();<br /> <br /> 읽기 전용 특성 DeviceInformation;<br /> 읽기 전용 특성 PlaybackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DeviceInformation {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DeviceInformation<br /> {<br /> 읽기 전용 특성 DomString os;<br /> <br /> <br /> 읽기 전용 속성 DomString id;<br /> readonly 특성 int densityDPI;<br /> readonly attribute int heightPixels;<br /> 읽기 전용 특성 int widthPixels; <br /> readonly 특성 boolean seekToKeyFrame;<br /> };<br /></p> </td> 
   <td><p>interface DeviceInformation<br /> {<br /> 읽기 전용 특성 DomString os;<br /> 읽기 전용 특성 int sdk;<br /> 읽기 전용 속성 DomString 모델;<br /> 읽기 전용 속성 DomString 제조업체;<br /> 읽기 전용 특성 DomString id;<br /> 읽기 전용 특성 intDPI;7/&gt; readonly 특성 int heightPixels;<br /> readonly 특성 int widthPixels;<br /> <br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 없음</td> 
   <td><p>interface LoadInfo<br /> {<br /> 읽기 전용 특성 DomString url;<br /> 읽기 전용 특성 int size;<br /> readonly attribute double downloadDuration;<br /> readonly attribute int periodIndex;<br /> readonly attribute double mediaDuration;<br /> readonly attribute short TRACK_TYPE_FRAGMENT;<br /> readonly 특성 short TRACK_TYPE_TRACK;<br /> 읽기 전용 속성 short TRACK_TYPE_MANIFEST;<br /> 읽기 전용 속성 짧은 유형;<br /> 읽기 전용 특성 DomString trackName;<br /> 읽기 전용 특성 DomString trackType;&lt;a1 2/&gt; readonly 특성 int trackIndex;<br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### {#view} 보기

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 없음</td> 
   <td><p>인터페이스 보기<br /> {<br /> 읽기 전용 특성 unsigned short x;<br /> 읽기 전용 속성 unsigned short y;<br /> 읽기 전용 속성 unsigned short width;<br /> 읽기 전용 속성 unsigned 짧은 높이;<br /> void setSize(unsigned width, 짧은 높이);<br /> void setPos(unsigned x, short y );<br /> }<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### 재생 정보 {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly 특성 double timeToFirstByte;<br /> readonly 특성 double timeToLoad;<br /> readonly 특성 double timeToStart;<br /> readonly attribute double timeToFail;<br /> readonly attribute intSecondsPlayed; <br /> readonly 특성 int totalSecondsSpent;<br /> readonly 특성 double frameRate;<br /> readonly attribute int droppedFrameCount;<br /> readonly attribute int indifiedBandwidth;<br /> readonly attribute int bitrateTime;<br /> 읽기 전용 특성 double buffer11/&gt; readonly 특성 int bufferLength;<br /> readonly 특성 int emptyBufferCount;<br /> readonly 특성 double bufferingTime;<br /> };<br /></p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly 특성 double timeToFirstByte;<br /> readonly 특성 double timeToLoad;<br /> readonly 특성 double timeToStart;<br /> readonly attribute double timeToFail;<br /> readonly attribute intSecondsPlayed; <br /> readonly 특성 int totalSecondsSpent;<br /> readonly 특성 double frameRate;<br /> readonly attribute int droppedFrameCount;<br /> <br /> readonly attribute int bitrateTime;<br /> readonly attribute double bufferTime;<br /> readonly attribute bufferAttribute length;<br /> readonly 특성 int emptyBufferCount;<br /> readonly 특성 double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 설명서를 참조하십시오.
