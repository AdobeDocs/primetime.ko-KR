---
title: TVSDK 변환 - JavaScript용 1.3-2.0
seo-title: TVSDK 변환 - JavaScript용 1.3-2.0
description: 많은 메서드 서명 및 API 요소 이름이 2.0에 대해 변경되었습니다.이 표를 검토하여 모든 API 변경 사항을 확인합니다.
seo-description: 많은 메서드 서명 및 API 요소 이름이 2.0에 대해 변경되었습니다.이 표를 검토하여 모든 API 변경 사항을 확인합니다.
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# TVSDK 변환 - JavaScript용 1.3-2.0 {#tvsdk-conversion-to-for-javascript}

많은 메서드 서명 및 API 요소 이름이 2.0에 대해 변경되었습니다.이 표를 검토하여 모든 API 변경 사항을 확인합니다.

## JavaScript에서 콜백 함수 구현 {#implement-callback-functions-in-javascript}

메서드 설명서의 주석에서는 구현해야 하는 콜백에 대한 서명을 제안합니다.

JavaScript의 경우 API 구문은 웹 ID를 기반으로 합니다. TVSDK 인터페이스의 경우 메서드 이름을 methodName() *이라고*&#x200B;합니다. 응용 프로그램에서 구현할 메서드의 경우 ** methodNameCallbackFunc라는 읽기/쓰기 특성이 인터페이스에 추가되고 응용 프로그램에서 메서드를 구현하는 함수를 가리키도록 설정해야 합니다. 예:

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

## 2.0에 대한 광고 워크플로우 API 요소 변경 {#advertising-workflow-api-element-changes-for}

다음 표에서는 JavaScript TVSDK에 대한 광고 워크플로우 API 요소를 버전 1.3과 2.0 간에 비교합니다.

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
* AdBreakTimelineItem/AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
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
   <td><p> <strong>TimedMetadata</strong>:interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0;부호 없는 짧은 METADATA_TYPE_ID3 = 1 ; <br /><br /> 읽기 전용 속성, 부호 없는 짧은 유형; <br /> 읽기 전용 속성에 대한 시간이 오래 걸립니다.<br /> readonly 특성 DomString id;<br /> readonly 특성 DomString name;<br /> readonly 특성 DomString 컨텐츠;읽기 전용 속성 개체 메타데이터; <br /><br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0;<br /> const unsigned short METADATA_TYPE_ID3 = 1;<br /> readonly 특성 unsigned short metadataType;<br /> 읽기 전용 속성(장시간)<br /> readonly 속성 long id;<br /> readonly 특성 DomString name;<br /> 읽기 전용 속성 개체 메타데이터; <br /><br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface TimedMetadataList {<br /> readonly 특성 unsigned long length;<br /> getter TimedMetadata(서명되지 않은 긴 인덱스);<br /> };</p> </td> 
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
   <td><p>Interface AdSigningMode { const unsigned short MODE_DEFAULT, const unsigned short MODE_MANIFEST_CUE, <br /> const <br /> unsigned short MODE_SERVER_MAP, <br /> const short MODE_CUSTOM_RANGES <br /> <br /> };</p> </td> 
   <td>MetadataKeys::MANIFEST_CUE 키를 대체합니다.</td> 
  </tr> 
 </tbody> 
</table>

### 광고 메타데이터 {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdvertisingMetadata { <br /> attribute AdSigningMode;속성 <br /> AdBreakWatchedPolicy adBreakAsViewed;부울 livePreroll <br /> ;부울 delayAdLoading ; <br /><br /> };</p> </td> 
   <td>이 기능은<p>MetadataKeys::ADVERTISING_METADATA</p> key.</td> 
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
   <td><p>인터페이스 CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE;부호 없는 <br /> 짧은 TYPE_DELETE_RANGE;부호 없는 <br /> 짧은 TYPE_REPLACE_RANGE;부호 없는 짧은 속성; <br /><br /> 속성 boolean adjustSeekPosition;TimeRangeList <br /> timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> attribute unsigned long begin; <br /> 읽기 전용 속성, 부호 없는 긴 끝; <br /> 속성 서명되지 않은 긴 기간unsigned long replaceDuration <br /> 속성; <br /> };</p> </td> 
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
   <td><p>인터페이스 배치 { <br /> const unsigned short TYPE_MID_ROLL;부호 없는 <br /> 짧은 TYPE_PRE_ROLL;부호 없는 <br /> 짧은 TYPE_POST_ROLL;서명되지 않은 <br /> 짧은 TYPE_SERVER_MAP;부호 없는 짧은 TYPE_CUSTOM_RANGE <br /> ;<br /> readonly 속성 unsigned short type; <br /> 읽기 전용 속성에 대한 시간이 오래 걸립니다. <br /> 읽기 전용 속성(긴 기간)서명되지 <br /> 않은 짧은 MODE_DEFAULT;서명되지 <br /> 않은 짧은 MODE_INSERT;서명되지 <br /> 않은 짧은 MODE_REPLACE; <br /> const unsigned short MODE_DELETE;서명되지 <br /> 않은 짧은 MODE_MARK;서명되지 <br /> 않은 짧은 MODE_FREE_REPLACE; <br /> 읽기 전용 속성 서명되지 않은 짧은 모드;읽기 전용 <br /> 속성 TimeRange; <br /> };</p> </td> 
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
   <td><p>interface Opportunity { <br /> readonly attribute DomString id;읽기 <br /> 전용 속성 배치;읽기 전용 속성 <br /> 개체 설정;readonly 특성 customParameters; <br /><br /> }; </p> </td> 
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
   <td><p>인터페이스 예약 { <br /> readonly attribute TimeRange; <br /> 읽기 전용 속성 장기 보류 <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 타임라인/타임라인 항목/타임라인 마커 {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>타임라인</strong>:인터페이스 타임라인 <br /> { readonly attribute TimelineMarkerList timelineMarkers;readonly 특성 TimelineItemList timelineItems; <br /> double convertToLocalTime( double time); <br /> double convertToVirtualTime( double time); <br /><br /> };</p> </td> 
   <td><p>인터페이스 타임라인 {<br /> 읽기 전용 속성 TimelineMarkerList timelineMarkers;<br /><br /><br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>:interface TimelineItem:<br /> TimelineMarker {<br /> readonly attribute long id;readonly 특성 TimeRange virtualRange; <br /> readonly 속성 <br /> TimeRange localRange; <br /> 읽기 전용 속성 부울 표시 <br /> readonly 속성 boolean temporary. <br /> }; </p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><strong>타임라인 마커</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface TimelineMarker {<br /> readonly 특성 double time;<br /> readonly 속성 double duration<br /> };</p> </td> 
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
   <td><p>interface AdBreak {<br /> <br /> 읽기 <br /> 전용 <br /> 특성 이중 지속 시간;<br /> readonly 속성 AdList 광고;<br /> 읽기 <br /> <br /> 전용 특성 AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> readonly 특성 double time;<br /> readonly 속성 double replaceDuration;<br /><br /> 읽기 전용 속성 이중 지속 시간<br /> readonly 속성 AdList adList;<br /> readonly 특성 DomString 데이터; <br /><br /><br /> }; </p> </td> 
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
   <td><p> <strong>광고</strong>:인터페이스 광고 {<br /> readonly attribute AdAsset primaryAsset;<br /> readonly 특성 AdAssetList companionAssets;<br /><br /> 읽기 전용 속성 이중 지속 시간<br /> readonly 특성 DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NEXINE = 1 ;<br /><br /> readonly 특성 unsigned short adType;<br /> readonly 특성 AdInsertionType adInsertionType; <br /> 읽기 <br /> 전용 속성 부울 클릭 가능; <br /> readonly 속성 부울 isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>인터페이스 광고 {<br /> readonly attribute AdAsset primaryAsset;<br /> readonly 특성 AdAssetList companionAssets;<br /><br /> 읽기 전용 속성 이중 지속 시간<br /> readonly 특성 DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NEXINE = 1 ;<br /><br /> 읽기 전용 속성, 부호 없는 짧은 유형;<br /> readonly 특성 AdInsertionType insertionType;읽기 <br /> 전용 속성 개체 추적기;<br /><br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface AdAsset {<br /> readonly 특성 DomString id;<br /> readonly 속성 double duration<br /> readonly 특성 MediaResource;<br /> readonly 속성 AdClick adClick;<br /> readonly 속성 개체 메타데이터;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface AdClick {<br /> readonly attribute DomString id;<br /> readonly 속성 DomString title;<br /> readonly 속성 DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface AdList {<br /> readonly attribute unsigned long length;<br /> getter Ad(부호 없는 긴 색인);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>:(2.0에 대한 변경 없음)</td> 
   <td><p>interface AdAssetList {<br /> readonly 특성 unsigned long length;<br /> getter AdAsset(부호 없는 긴 인덱스);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:interface AdBannerAsset:AdAsset<br /> {<br /> readonly 특성 int width;<br /> readonly 특성 int height;<br /> readonly 특성 DomString staticUrl;<br /> readonly 속성 DomString height;<br /> readonly 속성 DomString width;<br /> };</p> </td> 
   <td> 2.0의 새로운 기능</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem/AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>:interface AdBreakTimelineItem:TimelineItem { <br /> readonly attribute AdBreak adBreak;읽기 전용 <br /> 특성 AdTimelineItemList 항목; <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>:interface AdTimelineItem:TimelineItem { <br /> readonly attribute AdBreak adBreak;광고 <br /> 읽기 전용 속성; <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>:interface AdBreakTimelineItemList { <br /> readonly 특성 unsigned long length;getter <br /> AdBreakTimelineItem(서명되지 않은 행 인덱스); <br /> };</p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPolicy {<br /> readonly attribute short AD_BREAK_POLICY_SKIP;<br /> readonly attribute short AD_BREAK_POLICY_PLAY;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> readonly attribute short AD_BREAK_POLICY_SKIP;<br /> readonly attribute short AD_BREAK_POLICY_PLAY;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakViewedPolicy {<br /> readonly attribute short AD_BREAK_AS_VIEWED_ON_BEGIN;<br /> readonly attribute short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly attribute short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> readonly attribute short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly attribute short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly attribute short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> readonly attribute short AD_POLICY_PLAY;<br /> readonly attribute short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly attribute short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;readonly attribute short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /><br /> readonly attribute short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> readonly attribute short AD_POLICY_PLAY;<br /> readonly attribute short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly attribute short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> readonly attribute short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> readonly attribute short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> readonly attribute AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> readonly 특성 AdTimelineItem adTimelineItem;<br /> readonly 특성 double currentTime;<br /> readonly 속성 doubleSeekToTime;<br /> readonly 속성 double rate<br /> readonly 속성 짧은 모드;//AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> readonly 특성 AdBreakPlacementList <br /> adBreakPlacement;<br /> adad 읽기 전용 속성;<br /> readonly 특성 double currentTime;<br /> readonly 속성 doubleSeekToTime;<br /> readonly 속성 double rate<br /> readonly 속성 짧은 모드;//AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 속성 개체 selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsViewed selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 속성 개체 selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 타임라인 작업 {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface TimelineOperation { <br /> readonly attribute Placement; <br /> };</p> </td> 
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
   <td><p>interface AdBreakPlacement :TimelineOperation {<br /> readonly attribute AdBreak adBreak;<br /> 읽기 전용 속성 배치;// From TimelineOperation<br /> readonly 특성 double time;<br /> readonly 속성 double duration<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> readonly 특성 AdBreak adBreak;<br /> 읽기 전용 속성 배치;<br /> readonly 속성 double time<br /> readonly 속성 double duration<br /> };</p> </td> 
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
   <td><p>interface AuditudeSettings :AdvertisingMetadata { <br /> attribute DomString zoneId;DomString mediaId <br /> ;DomString defaultMediaId <br /> ;DomString 도메인 <br /> ;특성 <br /> 개체 대상 정보;속성 <br /> customParameters;속성 <br /> Boolean creativePackingEnabled;<br /> 속성 Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>기능은 MetadataKeys::AUDITUDE_METADATA_KEY에서 제공되었습니다.</td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 Customization API 요소 변경 {#customization-api-element-changes-for}

다음 표에서는 버전 1.3과 2.0 간에 JavaScript TVSDK에 대한 사용자 정의 API 요소를 비교합니다.

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
   <td><p>interface MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> attribute StringList subscribeTags;<br /> 속성 <br /> StringList adTags;<br /> AdSigningMode adSignaturesMode <br /> <br /> 특성;<br /> attribute CustomRangeMetadata customRangeMetadata;<br /> attribute NetworkConfiguration networkConfiguration;<br /> attribute AdvertisingMetadata advertisingMetadata;<br /> attribute Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /> 속성 StringList <br /> <br /> adTags;<br /> attribute StringList subscribedTags;<br /> attribute MediaPlayerClientFactory clientFactory;<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem 항목);<br /> */<br /> 특성 개체 검색AdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem);<br /> */<br /> 특성 개체 검색AdPolicySelectorFunc;<br /> };</p> </td> 
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
   <td><p>interface NetworkConfiguration<br /> {<br /> attribute boolean forceNativeNetworking;<br /> 속성 부울 useRedirectedUrl;<br /> attribute Object cookieHeader;<br /> attribute boolean readSetCookieHeader;<br /> attribute int masterUpdateInterval;속성 부울 useCookieHeaderForAllRequests; <br /><br /> attribute int readLimit;<br /> };</p> </td> 
   <td>1.3에서 이 기능 중 일부는 MetadataKeys에서 제공했습니다</td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 DRM API 요소 변경 {#drm-api-element-changes-for}

다음 표에서는 JavaScript TVSDK에 대한 DRM API 요소를 버전 1.3과 2.0 간에 비교합니다.

이 항목의 표:

* DRM 워크플로우 초기화
* DRMAcquireLicenseSettings/DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### DRM 워크플로우 초기화 {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>DRM 워크플로우를 시작하려면 애플리케이션에서 AdobePSDK.initiateDRMWorkflow를 호출해야 합니다. 이 호출이 없으면 DRM 비디오가 재생되지 않습니다.<p>인터페이스 AdobePSDK<br /> {<br /> voidDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> 부울 privacyModeOn);<br /> };</p> </td> 
   <td>초기화가 내부에서 수행되었으며 명시적 호출이 필요하지 않았습니다.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0은 변경되지 않습니다. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| 2.0은 변경되지 않습니다. | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int anonymous = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0은 변경되지 않습니다.</td> 
   <td><p>interface DRMMetadata<br /> {<br /> readonly 특성 DomString serverUrl;<br /> readonly 특성 DomString licenseId;<br /> readonly 특성 DRMPolicyArray 정책; <br /> };</p> </td> 
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
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly attribute int playbackPeriodInSeconds;<br /> readonly 특성 long playbackStartDate;<br /> readonly 특성 long playbackEndDate;<br /> };</p> </td> 
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
   <td>2.0은 변경되지 않습니다.</td> 
   <td><p>interface DRMLicense {<br /> readonly attribute Uint8Array bytes;<br /> readonly 속성 licenseStartDate;<br /> readonly 속성 licenseEndDate;<br /> readonly 특성 offlineStorageStartDate;<br /> readonly 특성 offlineStorageEndDate;readonly 특성 DomString serverUrl; <br /><br /> readonly 특성 DomString licenseID;<br /> readonly 특성 DomString policyID;<br /> readonly 특성 DRMPlaybackTimeWindow playbackTimeWindow;<br /> readonly 속성 customProperties;<br /> }; </p> </td> 
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
   <td><p>interface DRMLicenseDomain {<br /> readonly 특성 DomString authenticationDomain;<br /> readonly 특성 DRMAuthenticationMethod authenticationMethod;readonly 특성 DomString serverUrl; <br /><br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> readonly attribute DomString authDomain;<br /> readonly 특성 DRMAuthenticationMethod authMethod; <br /> readonly 특성 DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interface DRMPolicy<br /> {<br /> readonly 특성 DomString authenticationDomain;<br /> readonly 특성 DRMAuthenticationMethod authenticationMethod;<br /><br /> readonly 특성 DomString displayName;<br /> readonly 특성 DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {<br /> readonly 특성 DomString authDomain;<br /> readonly 특성 DRMAuthenticationMethod authMethod;<br /> readonly 특성 DomString dispName;<br /> readonly 특성 DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
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
   <td><p>interface DRMManager :EventTarget {<br /> void acquireLicense(DRMMetadata 메타데이터, <br /> DRMAcquireLicenseSettings 설정, <br /> DRMAquireLicenseListener);<br /> void acquirePreviewLicense(DRMMetadata 메타데이터, <br /> DRMAquireLicenseListener);<br /> void(DRMMetadata 메타데이터, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString 사용자, <br /> DomString 암호, <br /> DRMAuthenticateListener);<br /> DRMMetadata createMetadataFromBytes( <br /><br /> Uint8Array 배열, DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br /> attribute long maxOperationTime;<br /> void joinLicenseDomain( <br /> DRMLicenseDomain licenseDomain,<br /> boolean forceRefresh, <br /> <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /><br /> void resetDRM(DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> boolean commitImmediate, DRMReturnLicenseListener<br /> );<br /> void setAuthenticationToken(<br /> DRMMetadata 메타데이터, <br /> DomString authenticationDomain, <br /> Uint8Array 토큰, <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>interface DRMManager :EventTarget {<br /> void acquireLicense(DRMMetadata 메타데이터, <br /> DRMAcquireLicenseSettings 설정, <br /> EventContext eventContext);<br /> void acquirePreviewLicense(DRMMetadata 메타데이터, <br /> EventContext eventContext);<br /> void(DRMMetadata 메타데이터, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString 사용자, <br /> DomString 암호, <br /> EventContext eventContext);<br /> DRMMetadata <br /> createMetadataFromBytes(<br /> Uint8Array 배열, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> attribute long maxOperationTime;<br /> void joinLicenseDomain( <br /> DRMLicenseDomain licenseDomain,<br /> boolean forceRefresh, <br /> <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> void resetDRM(EventContext eventContext); <br /><br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> boolean commitImmediate, EventContext<br /> eventContext);<br /> void setAuthenticationToken(<br /> DRMMetadata 메타데이터, <br /> DomString authenticationDomain, <br /> Uint8Array 토큰, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMErrorListener : <br /> 공용 psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils:PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /><br /> 보호:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>DRMManger의 비동기 메서드 중 하나에 오류가 발생하는 경우</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMOperationCompleteListener : <br /> 공용 DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete() = 0;<br /><br /> 보호:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>DRM의 초기화가 완료되면</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>joinLicenseDomain() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>leaveLicenseDomain() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEVENTDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>resetDRM() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>setAuthenticationTokenSet() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>storeLicenseBytes() 작업이 성공적으로 완료되면</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMAuthenticateListener : <br /> 공용 DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImutableByteArray* <br /> authenticationToken) = 0;<br /><br /> 보호:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>DRMManager::authenticate 메서드 호출이 성공한 경우</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMAquireLicenseListener: <br /> 공용 DRMErrorListener {<br /> public:<br /> virtual void onLicenseAcquisition(const DRMLicense*) = 0;<br /><br /> 보호:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMPreviewLicenseObtained<p>/ DRMLicenseObtainedEvent</p> <p>DRMManager::acquirePreviewLicense 메서드 호출이 성공한 경우</p> </li> 
     <li>kEventDRMLicenseObtained<p>/ DRMLicenseObtainedEvent</p> <p>DRMManager::acquireLicense 메서드 호출이 성공한 경우</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMReturnLicenseListener: <br /> 공용 DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned) = 0;<br /><br /> 보호:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>이벤트/인터페이스/설명 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>DRMManager::returnLicense 메서드 호출이 성공한 경우</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 일반 재생 API 요소 변경 {#generic-playback-api-element-changes-for}

이 표에서는 JavaScript TVSDK 1.3과 2.0 간의 일반 재생 API 요소를 비교합니다.

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
   <td><p>interface MediaResource {<br /> attribute DomString url;부호 없는 짧은 속성; <br /><br /> 속성 개체 메타데이터;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> attribute DomString url;<br /> attribute DomString type;<br /> 속성 개체 메타데이터;<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay( 이중 위치);<br /> void play();<br /> void pause();<br /> void seek( double position);<br /> void seekToLocal( 이중 위치);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaPlayerItem);<br /> void replaceCurrentResource(MediaResource 소스, <br /> MediaPlayerItemConfig);void suspend(); <br /><br /> void restore();<br /> void notifyClick();<br /> readonly 속성 <br /> TimeRange playbackRange;<br /> readonly 속성 TimeRange searchableRange;<br /> readonly 특성 double currentTime;<br /> readonly 특성 double localTime;<br /> readonly 속성 TimeRange bufferedRange;<br /> readonly 특성 DRMManager drmManager;<br /> readonly 특성 MediaPlayerItem currentItem;<br /> // PlayerStatus <br /> const<br /> <br /> <br /> unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEARCHING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /><br /> 읽기 전용 속성 서명되지 않은 짧은 상태;<br /> 부호 없는 짧은 볼륨 속성; <br /><br /> attribute ABRConcontrolParameters abrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /><br /> const unsigned short VISIBLE;//CC 가시성<br /> const unsigned short INVISIBLE;//CC 가시성<br /> 속성에 서명되지 않은 짧은 가시성;<br /> attribute TextFormat ccStyle;<br /> readonly attribute PlaybackMetrics playbackMetrics;<br /> 속성 이중 속도; <br /><br /> attribute MediaPlayerView;<br /> readonly 속성 타임라인;<br /> attribute double currentTimeUpdateInterval; <br /> // 이 설정은 2.0<br /> };에 대해 지원되지 않습니다.</p> </td> 
   <td><p>interface MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay( int position);<br /> void play();<br /> void pause();<br /> void seek( int position);<br /> void seekToLocalTime( int position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaResource source);<br /><br /><br /><br /><br /><br /> readonly <br /> 속성 TimeRange playbackRange;<br /> readonly 속성 TimeRange searchableRange;<br /> readonly 특성 double currentTime;<br /> readonly 특성 double localTime;<br /> readonly 속성 TimeRange bufferedRange;<br /> readonly 특성 DRMManager drmManager;<br /> readonly 특성 MediaPlayerItem currentItem;<br /> // PlayerState <br /><br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEARCHING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> readonly 속성 unsigned short state;<br /> 부호 없는 짧은 볼륨 속성; <br /><br /> attribute ABRConcontrolParameters abrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /><br /> 읽기 전용 부호 없는 짧은 VISIBLE;//CC 가시성의<br /> 경우 읽기 전용 서명되지 않은 짧은 INVISIBLE;//CC 가시성<br /> 속성에 서명되지 않은 짧은 가시성;<br /> attribute TextFormat ccStyle;<br /> readonly attribute PlaybackMetrics playbackMetrics;<br /> attribute MediaPlayerConfig mediaPlayerConfig;<br /> 속성 이중 속도;<br /> attribute MediaPlayerView;<br /> readonly 속성 타임라인;<br /><br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus는<br /> 서명되지 않은 짧은 PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEARCHING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

#### MediaPlayer에서 지원되는 이벤트 {#events-supported-by-mediaplayer}

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
   <td>준비됨</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>미디어 플레이어 항목이 업데이트되는 경우</p> </td> 
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
   <td>adBreakSwitched</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSwitched</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClicked<br /> 사용자가 광고를 클릭할 때.</td> 
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
   <td>seekPositionAdjust<br /> 검색 위치가 내부 또는 외부 규칙으로 조정될 때.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audio<br /> 업데이트미디어 플레이어 항목이 업데이트될 때 재생 시간에만 감지할 수 있는 오디오 트랙을 포함하는 특정 스트림의 경우 새 오디오 트랙을 사용할 수 있을 때 이 이벤트가 발생합니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>캡션 <br /> 업데이트미디어 플레이어 항목이 업데이트되면 실시간/선형 스트림의 경우 클라이언트는 미디어 리소스를 정기적으로 새로 고쳐서 사용 가능한 새로운 컨텐츠를 감지해야 합니다. 이러한 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>master <br /> 업데이트됨 미디어 플레이어 항목이 업데이트되면 실시간/선형 스트림의 경우 클라이언트는 미디어 리소스를 정기적으로 새로 고쳐서 사용 가능한 새로운 컨텐츠를 감지해야 합니다. 이러한 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRange<br /> 업데이트된 미디어 플레이어 항목이 업데이트되면 실시간/선형 스트림의 경우 클라이언트는 미디어 리소스를 정기적으로 새로 고쳐서 사용 가능한 새로운 컨텐츠를 감지해야 합니다. 이러한 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>Timed<br /> Event 시간 이벤트가 생성되면 전송됩니다.</td> 
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
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_REVOR = 0;<br /> const unsigned short ABR_POLICY_MODERATE = 1;<br /> const unsigned short ABR_POLICY_AGGREGATIVE = 2;<br /> 부호 없는 짧은 <br /> 속성 정책;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_REVOR = 0;<br /> const unsigned short ABR_POLICY_MODERATE = 1;<br /> const unsigned short ABR_POLICY_AGGREGATIVE = 2;<br /> 부호 없는 짧은 <br /> 속성 정책;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /><br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /><br /> <br /> };</p> </td> 
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
   <td>2.0에 대한 변경 사항 없음</td> 
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0;<br /> const unsigned short COLOR_BLACK = 1;<br /> const unsigned short COLOR_GRAY = 2;<br /> const unsigned short COLOR_WHITE = 3;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4;<br /> const unsigned short COLOR_DARK_RED = 5;<br /> const unsigned short COLOR_RED = 6;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11;<br /> const unsigned short COLOR_BLUE = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13;<br /> const unsigned short COLOR_DARK_YELLOW = 14;<br /> const unsigned short COLOR_YELLOW = 15;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16;<br /> const unsigned short COLOR_DARK_MAGENTA = 17;<br /> const unsigned short COLOR_MAGENTA = 18;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19;<br /> const unsigned short COLOR_DARK_CYAN = 20;<br /> const unsigned short COLOR_CYAN = 21;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22;<br /><br /> readonly 특성 unsigned short fontColor;<br /> readonly 특성 unsigned short backgroundColor;<br /> readonly 특성 unsigned short fillColor;<br /> readonly 특성 unsigned short edgeColor;<br /> // Size <br /><br /> const unsigned short SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1;<br /> const unsigned short SIZE_MEDIUM = 2;<br /> const unsigned short SIZE_LARGE = 3 ;<br /><br /> 읽기 전용, 부호 없는 짧은 크기,<br /> // FontEdge <br /><br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2;<br /> const unsigned short FONT_EDGE_LLUD = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6;<br /> readonly 특성 unsigned short fontEdge;<br /> // Font <br /><br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3;<br /> const unsigned short FONT_CANCEIVE = 4 ;<br /> const unsigned short FONT_CUR시브가 5 ;<br /> const unsigned short FONT_SMALL_CAPITALS = 6;<br /> readonly 속성 unsigned short font;<br /> readonly 속성 unsigned short fontOpacity;<br /> readonly 특성 unsigned short backgroundOpacity;<br /> readonly 속성 unsigned short fillOpacity;<br /> readonly 특성 unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
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
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource resource, long resourceId,<br /> ItemLoaderListener, <br /> MediaPlayerItemConfig);<br /> void cancel();<br /> readonly 특성 MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 미디어 특성 API 요소 변경 {#media-characteristics-api-element-changes-for}

다음 표에서는 버전 1.3과 2.0 간에 C++ TVSDK의 미디어 특성 API 요소를 비교합니다.

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
   <td><p>interface MediaPlayerItem {<br /> readonly 특성 MediaResource;<br /> readonly 특성 long resourceId;<br /> readonly 속성 boolean live;<br /><br /> readonly 속성 boolean hasAlternateAudio;<br /> readonly 특성 AudioTrackList audioTracks;<br /> readonly 속성 AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack); <br /> readonly <br /> 속성 부울 hasClosedCaptions;<br /> readonly 특성 ClosedCaptionsTrackList closedCaptionsTracks;<br /> readonly 특성 ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack); <br /> readonly <br /> 특성 부울 hasTimedMetadata;<br /> readonly 특성 TimedMetadataList timedMetadata;<br /> readonly 속성 boolean dynamic;<br /><br /> readonly 속성 boolean isProtected;<br /> readonly 특성 DRMMetadataInfoList drmMetadataInfos;<br /> readonly 특성 ProfileList 프로필;<br /> readonly 속성 selectedProfile;<br /><br /> readonly 속성 boolean trickPlaySupported;<br /> readonly 속성 FloatArray availablePlaybackRates;<br /> readonly 속성 float selectedPlaybackRate;<br /><br /> 읽기 전용 속성 <br /> MediaPlayer;<br /> readonly 특성 MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>interface MediaPlayerItem {<br /> readonly 특성 MediaResource;<br /> readonly 특성 long resourceId;<br /> readonly 속성 boolean live;<br /><br /> readonly 속성 boolean hasAlternateAudio;<br /> readonly 특성 AudioTrackList audioTracks;<br /> attribute AudioTrack selectedAudioTrack;<br /><br /> readonly <br /> 속성 부울 hasClosedCaptions;<br /> readonly 특성 ClosedCaptionsTrackList ccTracks;<br /> attribute ClosedCaptionsTrack selectedCCTrack;<br /><br /> readonly <br /><br /> 특성 부울 hasTimedMetadata;<br /> readonly 특성 TimedMetadataList timedMetadata;<br /> readonly 속성 boolean dynamic;<br /><br /> readonly 속성 boolean isProtected;<br /> readonly 특성 DRMMetadataInfoList drmMetadataInfos;<br /> readonly 특성 ProfileList 프로필;<br /><br /> readonly <br /> 속성 boolean trickPlaySupported;<br /> readonly 특성 Int32Array availablePlaybackRates;<br /> readonly 속성 StringList adTags; <br /><br /> readonly 속성 <br /> MediaPlayer mediaPlayer;<br /><br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 트랙/오디오 트랙/자막 트랙 {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 추적<br /> {<br /> readonly 특성 DomString 이름;<br /> readonly 특성 DomString 언어;<br /> readonly 속성 부울 기본값;<br /> readonly 속성 boolean autoSelect;<br /> }; </p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack :추적<br /> {<br /> readonly 특성 DomString 이름;//FromTrack<br /> readonly 특성 DomString 언어;//FromTrack<br /> readonly 특성 부울 기본값;// From Track<br /> readonly 속성 boolean autoSelect;//FromTrack<br /> <br /> readonly 속성 unsigned int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> readonly 특성 DomString name;<br /> readonly 특성 DomString 언어; <br /> readonly 속성 부울 기본값;<br /> readonly 속성 boolean autoSelect;<br /> readonly 속성 boolean forced.<br /><br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 사항 없음</td> 
   <td><p>interface AudioTrackList<br /> {<br /> readonly 특성 unsigned long length;<br /> getter AudioTrack(서명되지 않은 긴 인덱스);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack :추적<br /> {<br /> readonly 특성 DomString 이름;//FromTrack<br /> readonly 특성 DomString 언어;//FromTrack<br /> readonly 특성 부울 기본값;// FromTrack<br /> readonly 속성 boolean autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> readonly 특성 unsigned short serviceType;<br /> readonly 속성 boolean forced.<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> readonly 특성 DomString name;<br /> readonly 특성 DomString 언어;<br /> readonly 속성 부울 기본값;<br /><br /> <br /> 읽기 전용 속성 부울 값,<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 사항 없음</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> readonly 특성 unsigned long length;<br /> getter ClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
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
   <td>프로필:2.0에 대한 변경 사항 없음</td> 
   <td><p>인터페이스 프로필<br /> {<br /> readonly 특성 unsigned int width;<br /> readonly 속성 unsigned int height;<br /> readonly 특성 unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>프로필 목록:2.0에 대한 변경 사항 없음</td> 
   <td><p>interface ProfileList<br /> {<br /> readonly 특성 unsigned long length;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
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
   <td><strong>DRMMetadataInfo</strong>:2.0에 대한 변경 사항 없음</td> 
   <td><p>interface DRMMetadataInfo<br /> { <br /> readonly 특성 DRMMetadata 메타데이터;<br /> readonly 속성 long prefetchTimestamp;<br /> readonly 특성 TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0에 대한 변경 사항 없음</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> readonly 특성 unsigned long length;<br /> getter DRMMetadataInfo(서명되지 않은 긴 인덱스);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 다른 언어의 C++ 오류에 대한 예외 매핑 {#mapping-c-errors-to-exceptions-in-different-languages}

C++ 오류 코드를 다른 언어로 된 예외에 매핑할 수 있습니다.

C++ PSDK에는 API에 대한 &quot;throw 없음&quot; 정책이 있습니다. 대부분의 API 메서드는 PSDKErrorCode 값을 반환하여 메서드가 성공적으로 실행되었는지 여부를 나타냅니다. 비동기 오류는 오류 이벤트를 통해 알립니다.

ActionScript 및 JAVA SDK의 정책은 다릅니다. 대부분의 오류는 ArgumentError 또는 IllegalStateException을 throw하여 메서드의 동기 부분을 실행할 수 없음을 나타냅니다. 이러한 예외는 발견되지 않으며 응용 프로그램 코드는 예외를 처리합니다. 일반적으로 메서드 호출이 실패한 이유에 대한 유용한 정보를 전달합니다. 예를 들어 prepareToPlay 명령이 잘못된 상태에서 호출되면 다음 예외가 발생합니다.

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA는 일부 내부 개체가 잘못 만들어졌음을 나타내는 생성자의 예외를 발생시킵니다. 이러한 예외는 내부적으로 처리되며 응용 프로그램에 전파되지 않습니다. 예외 사항은 응용 프로그램에 전송되는 경고 알림에 포함됩니다

예를 들어, 수신된 광고 응답에 대해 유효한 미디어 파일을 찾을 수 없으면 유효한 광고 자산 개체 또는 광고를 만들 수 없습니다. 따라서 타임라인에 광고가 배치되지 않고 NotificationEvent.OperationFailed 알림이 전달됩니다.

AVE(Adobe Video Engine)로부터 비동기식으로 수신되는 오류 또는 경고 코드는 일반 이벤트로 응용 프로그램에 전달됩니다. 알림 이벤트에는 수신된 모든 오류 코드와 URL, 리소스 식별자, 핸들 등과 같은 추가 메타데이터가 포함됩니다. 오류가 심각하고 현재 미디어의 재생을 계속할 수 없는 경우 MediaPlayer는 ERROR 상태와 onStatusChanged 콜백 또는 MediaPlayerStatusChanged.STATUS_CHANGED 이벤트가 전달됩니다. 재생을 계속할 수 있으면 일반 알림 이벤트가 전달됩니다.

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
   <td>예외(코드 = 1, description = "INVALID_ARGUMENT" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>예외(코드 = 2, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>예외(코드 = 3, description = "ILLEGAL_STATE" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 4, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 5, description = "CREATION_FAILED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 5, description = "CREATION_FAILED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 7, description = "DATA_NOT_AVAILABLE" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 8, description = "SEEK_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 9, description = "UNSUPPORTED_FEATURE" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 10, description = "RANGE_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨)</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 11, description = "CODEC_NOT_SUPPORTED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 12, description = "MEDIA_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 13, description = "NETWORK_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error 또는 MediaPlayerNotification.Warning</td> 
   <td>MediaError 또는 NotificationEvent</td> 
   <td>예외(코드 = 14, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 15, description = "INVALID_SEEK_TIME" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 16, description = "AUDIO_TRACK_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 17, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 18, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨)</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 19, description = "GENERIC_ERROR" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외(코드 = 200, description = "PLAYBACK_OPERATION_FAILED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>예외(코드 = 201, description = "NATIVE_WARNING" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨)</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>예외(코드 = 202, description = "AD_RESOLVER_FAILED" 및 additionalInfo= &lt;이 예외를 발생시킨 메서드에 의해 전달됨&gt;)</td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 유틸리티 및 도우미 API 요소 변경 {#utility-and-helper-api-element-changes-for}

다음 표에서는 버전 1.3과 2.0 간에 JavaScript TVSDK에 대한 유틸리티 및 헬퍼 API 요소를 비교합니다.

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
   <td><p>인터페이스 버전<br /> {<br /> readonly 특성 DomString 버전;<br /> readonly 속성 DomString 설명;<br /> 읽기 전용 속성(장주)<br /> 읽기 전용 속성(부)<br /> readonly 속성 long revision.<br /> readonly 속성 long apiVersion;<br /> };</p> </td> 
   <td><p>인터페이스 버전<br /> {<br /> readonly 특성 DomString 버전;<br /> readonly 속성 DomString 설명;<br /> readonly 속성 DomString 주;<br /> readonly 특성 DomString minor;<br /> readonly 특성 DomString 개정;<br /> readonly 특성 DomString apiVersion;<br /> };</p> </td> 
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
   <td>2.0에 대한 변경 사항 없음</td> 
   <td><p>interface TimeRange<br /> {<br /> readonly 특성 unsigned long begin;<br /> readonly 속성 unsigned long end;<br /> readonly 속성 unsigned long duration.<br /> };</p> </td> 
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
   <td>2.0에 대한 변경 사항 없음</td> 
   <td><p>인터페이스 QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer);<br /> void detachMediaPlayer();<br /> readonly 특성 DeviceInformation deviceInformation; <br /><br /> readonly 속성 PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 장치 정보 {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DeviceInformation<br /> {<br /> readonly 특성 DomString os;<br /><br /> readonly <br /><br /> 특성 DomString id;<br /> readonly 특성 int densityDPI;<br /> readonly 특성 int heightPixels;<br /> readonly 특성 int widthPixels;<br /> readonly 특성 boolean seekToKeyFrame;<br /> };</p> </td> 
   <td><p>interface DeviceInformation<br /> {<br /> readonly 특성 DomString os;<br /> readonly 속성 int sdk;<br /> readonly 특성 DomString 모델;<br /> readonly 특성 DomString 제조업체;<br /> readonly 특성 DomString id;<br /> readonly 특성 int densityDPI;<br /> readonly 특성 int heightPixels;<br /> readonly 특성 int widthPixels;<br /><br /> };</p> </td> 
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
   <td>2.0에 대한 변경 사항 없음</td> 
   <td><p>interface LoadInfo<br /> {<br /> readonly 특성 DomString url;<br /> readonly 특성 int size;<br /> readonly 속성 double downloadDuration;<br /> readonly 특성 int periodIndex;<br /> readonly 속성 double mediaDuration;<br /> readonly 속성 short TRACK_TYPE_FRAGMENT;<br /> readonly attribute short TRACK_TYPE_TRACK;<br /> readonly 특성 short TRACK_TYPE_MANIFEST;<br /> readonly 속성 short type;<br /> readonly 특성 DomString trackName;<br /> readonly 특성 DomString trackType;<br /> readonly 특성 int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 보기 {#view}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 사항 없음</td> 
   <td><p>인터페이스 보기<br /> {<br /> readonly attribute unsigned short x;<br /> readonly 속성 unsigned short y;<br /> readonly 속성 unsigned short width;<br /> readonly 속성 unsigned short height;<br /><br /> void setSize(부호 없는 짧은 폭, 부호 없는 짧은 높이);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
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
   <td><p>interface PlaybackInformation<br /> {<br /> readonly 특성 double timeToFirstByte;<br /> readonly 속성 double timeToLoad;<br /> readonly 속성 double timeToStart;<br /> readonly 속성 double timeToFail;<br /> readonly 속성 int totalSecondsPlayed;<br /> readonly 속성 int totalSecondsSpent;<br /> readonly 특성 double frameRate;<br /> readonly 특성 int dropedFrameCount;<br /> readonly 특성 indifiedBandwidth;<br /> readonly 속성 int 비트 전송률;<br /> readonly 특성 double bufferTime;<br /> readonly 특성 int bufferLength;<br /> readonly 특성: emptyBufferCount;<br /> readonly 속성 double bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly 특성 double timeToFirstByte;<br /> readonly 속성 double timeToLoad;<br /> readonly 속성 double timeToStart;<br /> readonly 속성 double timeToFail;<br /> readonly 속성 int totalSecondsPlayed;<br /> readonly 속성 int totalSecondsSpent;<br /> readonly 특성 double frameRate;<br /> readonly 특성 int dropedFrameCount;<br /><br /> 읽기 전용 속성 int 비트 전송률;<br /> readonly 특성 double bufferTime;<br /> readonly 특성 int bufferLength;<br /> readonly 특성: emptyBufferCount;<br /> readonly 속성 double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 유용한 리소스 {#helpful-resources}

* Adobe Primetime 학습 및 지원 [페이지에서 전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.
