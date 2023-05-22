---
title: TVSDK 변환 - JavaScript용 1.3에서 2.0으로
description: 2.0에 대해 많은 메서드 시그니처 및 API 요소 이름이 변경되었습니다. 모든 API 변경 세부 사항을 보려면 다음 표를 검토하십시오.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
exl-id: 4b251e26-cee6-4d96-bb55-6c47195da4d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---

# TVSDK 변환 - JavaScript용 1.3에서 2.0으로 {#tvsdk-conversion-to-for-javascript}

2.0에 대해 많은 메서드 시그니처 및 API 요소 이름이 변경되었습니다. 모든 API 변경 세부 사항을 보려면 다음 표를 검토하십시오.

## JavaScript에서 콜백 함수 구현 {#implement-callback-functions-in-javascript}

메서드 설명서의 주석은 구현해야 하는 콜백에 대한 서명을 제안합니다.

JavaScript의 경우 API 구문은 웹 ID를 기반으로 합니다. TVSDK 인터페이스의 경우 메서드 이름이 호출됩니다. *methodName*(). 응용 프로그램에서 구현할 메서드의 경우 읽기/쓰기 속성이 호출됩니다. *methodName* CallbackFunc가 인터페이스에 추가되고 응용 프로그램에서 메서드를 구현하는 함수를 가리키도록 설정해야 합니다. 예:

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

## 2.0용 Advertising Workflow API 요소 변경 {#advertising-workflow-api-element-changes-for}

이 표에서는 버전 1.3과 2.0 간의 JavaScript TVSDK에 대한 Advertising Workflow API 요소를 비교합니다.

이 항목의 표:

* TimedMeta
* AdSignaling 모드
* AdvertisingMeta
* 사용자 지정 범위 메타데이터
* 시간 범위 바꾸기
* 배치
* 영업 기회
* 예약
* 타임라인/TimelineItem/TimelineMarker
* AdBreak
* 광고 / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy/AdBreakWatchedPolicy/AdPolicy/AdPolicyMode/AdPolicyInfo/AdPolicySelector
* 타임라인 작업
* 광고 브레이크 배치
* Auditude 설정

### TimedMeta {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMeta</strong>: 인터페이스 TimedMetadata {<br /> const 부호 없는 short METADATA_TYPE_TAG = 0 ; <br /> const 부호 없는 short METADATA_TYPE_ID3 = 1 ; <br /> 읽기 전용 특성 부호 없는 짧은 형식; <br /> 읽기 전용 속성 긴 시간;<br /> 읽기 전용 속성 DomString id;<br /> 읽기 전용 속성 DomString 이름;<br /> 읽기 전용 속성 DomString 콘텐츠; <br /> 읽기 전용 속성 객체 메타데이터<br /> }; </p> </td> 
   <td><p>인터페이스 TimedMetadata {<br /> const 부호 없는 short METADATA_TYPE_TAG = 0 ;<br /> const 부호 없는 short METADATA_TYPE_ID3 = 1 ;<br /> readonly 특성 부호 없는 short metadataType;<br /> 읽기 전용 속성 긴 시간;<br /> 읽기 전용 속성 long id;<br /> 읽기 전용 속성 DomString 이름;<br /> <br /> 읽기 전용 속성 객체 메타데이터<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetaList</strong>: (2.0에 대한 변경 내용 없음)</td> 
   <td><p>인터페이스 TimedMetadataList {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter TimedMetadata(부호 없는 긴 색인);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSignaling 모드 {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdSignalingMode { <br /> const 부호 없는 short MODE_DEFAULT, <br /> const 부호 없는 short MODE_MANIFEST_CUES , <br /> const 부호 없는 short MODE_SERVER_MAP , <br /> const 부호 없는 short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>이 URL은 MetadataKeys::MANIFEST_CUES 키를 대체합니다.</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMeta {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdvertisingMetadata { <br /> 속성 AdSignalingMode 모드; <br /> attribute AdBreakWatchedPolicy adBreakAsWatched; <br /> 속성 부울 livePreroll; <br /> 속성 부울 delayAdLoading ; <br /> };</p> </td> 
   <td>이 기능은에서 제공했습니다.<p>메타데이터 키::ADVERTISING_METADATA</p> 키.</td> 
  </tr> 
 </tbody> 
</table>

### 사용자 지정 범위 메타데이터 {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 CustomRangeMetadata { <br /> const 부호 없는 short TYPE_MARK_RANGE; <br /> const 부호 없는 short TYPE_DELETE_RANGE; <br /> const 부호 없는 short TYPE_REPLACE_RANGE; <br /> 특성 부호 없는 짧은 형식; <br /> 속성 부울 adjustSeekPosition; <br /> attribute TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 시간 범위 바꾸기 {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 ReplaceTimeRange { <br /> 특성 부호 없는 long begin; <br /> 읽기 전용 특성 부호 없는 긴 끝; <br /> 특성 부호 없는 긴 기간; <br /> 특성 부호 없는 long replaceDuration; <br /> };</p> </td> 
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
   <td><p>인터페이스 배치 { <br /> const 부호 없는 short TYPE_MID_ROLL; <br /> const 부호 없는 short TYPE_PRE_ROLL; <br /> const 부호 없는 short TYPE_POST_ROLL; <br /> const 부호 없는 short TYPE_SERVER_MAP; <br /> const 부호 없는 short TYPE_CUSTOM_RANGE;<br /> 읽기 전용 특성 부호 없는 짧은 형식; <br /> 읽기 전용 속성 긴 시간; <br /> 읽기 전용 속성 긴 기간; <br /> const 부호 없는 short MODE_DEFAULT; <br /> const 부호 없는 short MODE_INSERT; <br /> const 부호 없는 short MODE_REPLACE; <br /> const 부호 없는 short MODE_DELETE; <br /> const 부호 없는 short MODE_MARK; <br /> const 부호 없는 short MODE_FREE_REPLACE; <br /> 읽기 전용 특성 부호 없는 짧은 모드; <br /> 읽기 전용 특성 TimeRange 범위; <br /> };</p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 영업 기회 {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 영업 기회 { <br /> 읽기 전용 속성 DomString id; <br /> 읽기 전용 속성 배치; <br /> 읽기 전용 속성 객체 설정 <br /> 읽기 전용 속성 Object customParameters; <br /> }; </p> </td> 
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
   <td><p>인터페이스 예약 { <br /> 읽기 전용 특성 TimeRange 범위; <br /> 읽기 전용 속성 long hold; <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 타임라인/TimelineItem/TimelineMarker {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>타임라인</strong>: 인터페이스 타임라인 <br /> { readonly 특성 TimelineMarkerList timelineMarkers; <br /> readonly 속성 TimelineItemList timelineItems; <br /> double convertToLocalTime( double time); <br /> double convertToVirtualTime( double time); <br /> };</p> </td> 
   <td><p>인터페이스 타임라인 {<br /> readonly 속성 TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: 인터페이스 TimelineItem :<br /> 타임라인 마커 {<br /> 읽기 전용 속성 long id; <br /> 읽기 전용 특성 TimeRange virtualRange; <br /> readonly 특성 TimeRange localRange; <br /> 읽기 전용 속성 부울 감시; <br /> 읽기 전용 속성 부울 임시; <br /> }; </p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>: (2.0에 대한 변경 내용 없음)</td> 
   <td><p>인터페이스 TimelineMarker {<br /> 읽기 전용 속성 double time;<br /> 읽기 전용 속성 이중 기간;<br /> };</p> </td> 
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
   <td><p>인터페이스 AdBreak {<br /> <br /> <br /> <br /> 읽기 전용 속성 이중 기간;<br /> 읽기 전용 속성 광고 목록;<br /> <br /> <br /> readonly 속성 AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>인터페이스 AdBreak {<br /> 읽기 전용 속성 double time;<br /> readonly 속성 double replaceDuration;<br /> <br /> 읽기 전용 속성 이중 기간;<br /> 읽기 전용 속성 AdList adList;<br /> <br /> 읽기 전용 속성 DomString 데이터;<br /> <br /> }; </p> </td> 
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
   <td><p> <strong>광고</strong>: 인터페이스 광고 {<br /> 읽기 전용 속성 AdAsset primaryAsset;<br /> 읽기 전용 속성 AdAssetList companionAssets;<br /> <br /> 읽기 전용 속성 이중 기간;<br /> 읽기 전용 속성 DomString id;<br /> const 부호 없는 short ADTYPE_LINEAR = 0 ;<br /> const 부호 없는 short ADTYPE_NONLINEAR = 1 ;<br /> <br /> 읽기 전용 특성 부호 없는 short adType;<br /> readonly 속성 AdInsertionType adInsertionType; <br /> <br /> 읽기 전용 속성 부울 클릭 가능; <br /> 읽기 전용 특성 부울 isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>인터페이스 광고 {<br /> 읽기 전용 속성 AdAsset primaryAsset;<br /> 읽기 전용 속성 AdAssetList companionAssets;<br /> <br /> 읽기 전용 속성 이중 기간;<br /> 읽기 전용 속성 DomString id;<br /> const 부호 없는 short ADTYPE_LINEAR = 0 ;<br /> const 부호 없는 short ADTYPE_NONLINEAR = 1 ;<br /> <br /> 읽기 전용 특성 부호 없는 짧은 형식;<br /> readonly 속성 AdInsertionType insertionType; <br /> readonly 속성 개체 추적기;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (2.0에 대한 변경 내용 없음)</td> 
   <td><p>인터페이스 AdAsset {<br /> 읽기 전용 속성 DomString id;<br /> 읽기 전용 속성 이중 기간;<br /> 읽기 전용 속성 MediaResource 리소스;<br /> 읽기 전용 속성 AdClick adClick;<br /> 읽기 전용 속성 객체 메타데이터<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (2.0에 대한 변경 내용 없음)</td> 
   <td><p>인터페이스 AdClick {<br /> 읽기 전용 속성 DomString id;<br /> 읽기 전용 속성 DomString 제목;<br /> 읽기 전용 속성 DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (2.0에 대한 변경 내용 없음)</td> 
   <td><p>인터페이스 AdList {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter Ad(부호 없는 긴 색인);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (2.0에 대한 변경 내용 없음)</td> 
   <td><p>인터페이스 AdAssetList {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter AdAsset(부호 없는 긴 색인);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: 인터페이스 AdBannerAsset : AdAsset<br /> {<br /> readonly 속성 int width;<br /> readonly 속성 int 높이;<br /> readonly 속성 DomString staticUrl;<br /> 읽기 전용 속성 DomString 높이;<br /> 읽기 전용 속성 DomString 너비;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: 인터페이스 AdBreakTimelineItem : TimelineItem { <br /> 읽기 전용 속성 AdBreak adBreak; <br /> 읽기 전용 특성 AdTimelineItemList 항목; <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: 인터페이스 AdTimelineItem : TimelineItem { <br /> 읽기 전용 속성 AdBreak adBreak; <br /> 읽기 전용 속성 광고; <br /> }; </p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: 인터페이스 AdBreakTimelineItemList { <br /> 읽기 전용 특성 부호 없는 긴 길이; <br /> getter AdBreakTimelineItem(부호 없는 lo ng 인덱스); <br /> };</p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy/AdBreakWatchedPolicy/AdPolicy/AdPolicyMode/AdPolicyInfo/AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdBreakPolicy {<br /> 읽기 전용 속성 short AD_BREAK_POLICY_SKIP;<br /> 읽기 전용 속성 short AD_BREAK_POLICY_PLAY;<br /> 읽기 전용 속성 short AD_BREAK_POLICY_REMOVE;<br /> 읽기 전용 속성 short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> 인터페이스 AdPolicyConstants {<br /> 읽기 전용 속성 short AD_BREAK_POLICY_SKIP;<br /> 읽기 전용 속성 short AD_BREAK_POLICY_PLAY;<br /> 읽기 전용 속성 short AD_BREAK_POLICY_REMOVE;<br /> readonly 속성 short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> 인터페이스 AdBreakWatchedPolicy {<br /> readonly 속성 short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly 속성 short AD_BREAK_AS_WATCHED_ON_END;<br /> 읽기 전용 속성 short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> readonly 속성 short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly 속성 short AD_BREAK_AS_WATCHED_ON_END;<br /> 읽기 전용 속성 short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>인터페이스 광고 정책 {<br /> 읽기 전용 속성 short AD_POLICY_PLAY;<br /> readonly 속성 short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 읽기 전용 속성 short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; 읽기 전용 속성 short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> 읽기 전용 속성 short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> 읽기 전용 속성 short AD_POLICY_PLAY;<br /> readonly 속성 short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly 속성 short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> 읽기 전용 속성 short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> 읽기 전용 속성 short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdPolicyMode {<br /> readonly 속성 short AD_POLICY_MODE_PLAY;<br /> readonly 속성 short AD_POLICY_MODE_SEEK;<br /> readonly 속성 short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly 특성 short AD_POLICY_MODE_PLAY;<br /> readonly 속성 short AD_POLICY_MODE_SEEK;<br /> readonly 속성 short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdPolicyInfo {<br /> readonly 속성 AdBreakTimelineItemList <br /> adBreakTimelineItems<br /> 읽기 전용 특성 AdTimelineItem adTimelineItem;<br /> readonly 속성 double currentTime;<br /> readonly 속성 double seekToTime;<br /> 읽기 전용 속성 이중화 비율;<br /> 읽기 전용 속성 짧은 모드; //AdPolicyMode<br /> };</p> </td> 
   <td><p>인터페이스 AdPolicyInfo {<br /> readonly 속성 AdBreakPlacementList <br /> adBreakPlaces;<br /> 읽기 전용 속성 광고;<br /> readonly 속성 double currentTime;<br /> readonly 속성 double seekToTime;<br /> 읽기 전용 속성 이중화 비율;<br /> 읽기 전용 속성 짧은 모드; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreakToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute 개체 selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>인터페이스 AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreakToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute 개체 selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 특성 개체 selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
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
   <td><p>인터페이스 TimelineOperation { <br /> 읽기 전용 속성 배치 ; <br /> };</p> </td> 
   <td> (2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

### 광고 브레이크 배치 {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AdBreakPlacement : TimelineOperation {<br /> 읽기 전용 속성 AdBreak adBreak;<br /> 읽기 전용 속성 배치, // TimelineOperation에서<br /> 읽기 전용 속성 double time;<br /> 읽기 전용 속성 이중 기간;<br /> };</p> </td> 
   <td><p>인터페이스 AdBreakPlacement {<br /> 읽기 전용 속성 AdBreak adBreak;<br /> 읽기 전용 속성 배치;<br /> 읽기 전용 속성 double time;<br /> 읽기 전용 속성 이중 기간;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Auditude 설정 {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AuditudeSettings : AdvertisingMetadata { <br /> 특성 DomString zoneId; <br /> 특성 DomString mediaId; <br /> attribute DomString defaultMediaId ; <br /> 속성 DomString 도메인 ; <br /> 속성 개체 targettingInfo ; <br /> attribute Object customParameters ; <br /> attribute Boolean creativePackingEnabled ;<br /> 속성 부울 showStaticBanners ;<br /> };</p> </td> 
   <td>기능이 MetadataKeys::AUDITUDE_METADATA_KEY에서 제공되었습니다.</td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 사용자 지정 API 요소 변경 사항 {#customization-api-element-changes-for}

이 표에서는 버전 1.3과 2.0 간의 JavaScript TVSDK에 대한 사용자 지정 API 요소를 비교합니다.

이 항목의 표:

* 미디어 플레이어 항목 구성
* ContentFactory
* 네트워크 구성

### 미디어 플레이어 항목 구성 {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> 속성 StringList subscribeTags;<br /> <br /> 특성 StringList adTags;<br /> <br /> <br /> attribute AdSignalingMode adSignalingMode;<br /> 특성 CustomRangeMetadata customRangeMetadata;<br /> attribute NetworkConfiguration networkConfiguration;<br /> attribute AdvertisingMetadata advertisingMetadata;<br /> 속성 부울 useHardwareDecoder;<br /> };</p> </td> 
   <td><p>인터페이스 MediaPlayerConfig {<br /> <br /> <br /> <br /> 특성 StringList adTags;<br /> 속성 StringList subscribedTags;<br /> 특성 MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>인터페이스 ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem 항목);<br /> */<br /> 특성 개체 retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>인터페이스 MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem 항목);<br /> */<br /> 특성 개체 retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 네트워크 구성 {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 NetworkConfiguration<br /> {<br /> 속성 부울 forceNativeNetworking;<br /> 속성 부울 useRedirectedUrl;<br /> attribute Object cookieHeader;<br /> 속성 부울 readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> 속성 부울 useCookieHeaderForAllRequests;<br /> attribute int readLimit;<br /> };</p> </td> 
   <td>1.3에서 이 기능 중 일부는 MetadataKeys에서 제공되었습니다</td> 
  </tr> 
 </tbody> 
</table>

## 2.0용 DRM API 요소 변경 사항 {#drm-api-element-changes-for}

이 표에서는 버전 1.3과 2.0 간의 JavaScript TVSDK용 DRM API 요소를 비교합니다.

이 항목의 표:

* DRM 워크플로우 초기화
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* 정책
* DRMMmanager

### DRM 워크플로우 초기화 {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>DRM 워크플로우를 시작하려면 애플리케이션에서 AdobePSDK.initiateDRMWorkflow를 호출해야 합니다. 이 호출이 없으면 DRM 비디오가 재생되지 않습니다.<p>인터페이스 AdobePSDK<br /> {<br /> 무효 initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString 앱 버전, <br /> 부울 privacyModeOn);<br /> };</p> </td> 
   <td>내부적으로 초기화가 수행되었으며 명시적인 호출이 필요하지 않았습니다.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0은 변경되지 않습니다. | enum DRMAcquireLicenseSettings <br>{<br> const 부호 없는 int FORCE_REFRESH = 0;<br> const 부호 없는 int LOCAL_ONLY = 1;<br> const 부호 없는 int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| 2.0은 변경되지 않습니다. | enum DRMAuthenticationMethod <br>{<br> const 부호 없는 int UNKNOWN = 0;<br> const 부호 없는 int ANONYMOUS = 1;<br> const 부호 없는 int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0은 변경되지 않습니다.</td> 
   <td><p>인터페이스 DRMMetadata<br /> {<br /> 읽기 전용 속성 DomString serverUrl;<br /> 읽기 전용 속성 DomString licenseId;<br /> 읽기 전용 속성 DRMPolicyArray 정책; <br /> };</p> </td> 
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
   <td><p>인터페이스 DRMPlaybackTimeWindow {<br /> readonly 속성 int playbackPeriodInSeconds;<br /> readonly 속성 long playbackStartDate;<br /> readonly 속성 long playbackEndDate;<br /> };</p> </td> 
   <td><p>인터페이스 DRMPlaybackTimeWindow {<br /> readonly 속성 int periodInSeconds;<br /> readonly 속성 int startDate;<br /> readonly 속성 int endDate;<br /> };</p> </td> 
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
   <td><p>인터페이스 DRMLicense {<br /> readonly 속성 Uint8Array 바이트;<br /> 읽기 전용 속성 Date licenseStartDate;<br /> 읽기 전용 속성 Date licenseEndDate;<br /> readonly 속성 Date offlineStorageStartDate;<br /> readonly 속성 Date offlineStorageEndDate; <br /> 읽기 전용 속성 DomString serverUrl;<br /> 읽기 전용 속성 DomString licenseID;<br /> 읽기 전용 속성 DomString policyID;<br /> readonly 속성 DRMPlaybackTimeWindow playbackTimeWindow;<br /> 읽기 전용 속성 Object customProperties;<br /> }; </p> </td> 
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
   <td><p>인터페이스 DRMLicenseDomain {<br /> readonly 속성 DomString authenticationDomain;<br /> 읽기 전용 속성 DRMAuthenticationMethod authenticationMethod; <br /> 읽기 전용 속성 DomString serverUrl;<br /> };</p> </td> 
   <td><p>인터페이스 DRMLicenseDomain {<br /> 읽기 전용 속성 DomString authDomain;<br /> 읽기 전용 속성 DRMAuthenticationMethod authMethod; <br /> readonly 속성 DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 정책 {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 DRMPolicy<br /> {<br /> readonly 속성 DomString authenticationDomain;<br /> 읽기 전용 속성 DRMAuthenticationMethod authenticationMethod;<br /> <br /> readonly 속성 DomString displayName;<br /> 읽기 전용 속성 DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>인터페이스 DRMPolicy<br /> {<br /> 읽기 전용 속성 DomString authDomain;<br /> 읽기 전용 속성 DRMAuthenticationMethod authMethod;<br /> 읽기 전용 속성 DomString dispName;<br /> 읽기 전용 속성 DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMmanager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 DRMManager : EventTarget {<br /> 무효 acquireLicense(DRMMetadata 메타데이터, <br /> DRMAcquireLicenseSettings 설정, <br /> DRMAquireLicenseListener);<br /> 무효 acquirePreviewLicense(DRMMetadata metadata, <br /> DRMAquireLicenseListener);<br /> 무효 인증(DRMMetadata 메타데이터, <br /> DomString url,<br /> DomString 및 인증 도메인, <br /> DomString 사용자, <br /> DomString 암호, <br /> DRMAuthenticateListener);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array 배열, DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br /> 특성 long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> 부울 forceRefresh, <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString 라이선스 ID, <br /> DomString policyID, <br /> 부울 commitImmediate,<br /> DRMRreturnLicenseListener);<br /> void setAuthenticationToken(<br /> DRMMetadata 메타데이터, <br /> DomString authenticationDomain, <br /> Uint8Array 토큰, <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>인터페이스 DRMManager : EventTarget {<br /> 무효 acquireLicense(DRMMetadata 메타데이터, <br /> DRMAcquireLicenseSettings 설정, <br /> EventContext eventContext);<br /> 무효 acquirePreviewLicense(DRMMetadata metadata, <br /> EventContext eventContext);<br /> 무효 인증(DRMMetadata 메타데이터, <br /> DomString url,<br /> DomString 및 인증 도메인, <br /> DomString 사용자, <br /> DomString 암호, <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array 배열, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> 특성 long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> 부울 forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString 라이선스 ID,<br /> DomString policyID, <br /> 부울 commitImmediate,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> DRMMetadata 메타데이터, <br /> DomString authenticationDomain, <br /> Uint8Array 토큰, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>클래스 DRMErrorListener : <br /> 공용 psdkutils::PSDKIinterfaceWithUserData {<br /> 공개:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> psdkutils:: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> 보호됨:<br /> 가상 ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>이벤트 / 인터페이스 / 설명 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>DRMManger의 비동기 메서드 중 하나에 오류가 발생하는 경우</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>클래스 DRMOperationCompleteListener : <br /> 공용 DRMErrorListener {<br /> 공개:<br /> virtual void onDRMOperationComplete() = 0;<br /> <br /> 보호됨:<br /> 가상 ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>이벤트 / 인터페이스 / 설명 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>DRM 초기화가 완료되면</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>joinLicenseDomain() 작업이 성공적으로 완료되는 경우.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>leaveLicenseDomain() 작업이 성공적으로 완료되는 경우.</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>resetDRM() 작업이 성공적으로 완료되면</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>setAuthenticationTokenSet() 작업이 성공적으로 완료된 경우.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>storeLicenseBytes() 작업이 성공적으로 완료되면.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>클래스 DRMAuthenticateListener : <br /> 공용 DRMErrorListener {<br /> 공개:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> 보호됨:<br /> 가상 ~DRMAuthenticationListener() {}<br /> }</p> </td> 
   <td>이벤트 / 인터페이스 / 설명 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>DRMManager::authenticate 메서드 호출이 성공하면</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>클래스 DRMAquireLicenseListener: <br /> 공용 DRMErrorListener {<br /> 공개:<br /> virtual void onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> 보호됨:<br /> 가상 ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>이벤트 / 인터페이스 / 설명 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>DRMManager::acquirePreviewLicense 메서드 호출이 성공하면</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>DRMManager::acquireLicense 메서드 호출이 성공하면</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>클래스 DRMReturnLicenseListener: <br /> 공용 DRMErrorListener {<br /> 공개:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned ) = 0;<br /> <br /> 보호됨:<br /> 가상 ~DRMRreturnLicenseListener() {}<br /> };</p> </td> 
   <td>이벤트 / 인터페이스 / 설명 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>DRMManager::returnLicense 메서드 호출이 성공하면</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 일반 재생 API 요소 변경 사항 {#generic-playback-api-element-changes-for}

이 표에서는 JavaScript TVSDK 1.3과 2.0 간의 일반 재생 API 요소를 비교합니다.

이 항목의 표:

* MediaResource
* MediaPlayer
* ABRControlParameters
* 버퍼 제어 매개변수
* 텍스트 형식
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 MediaResource {<br /> attribute DomString url; <br /> 특성 부호 없는 짧은 형식;<br /> 속성 개체 메타데이터;<br /> const 부호 없는 short TYPE_HLS;<br /> const 부호 없는 short TYPE_HDS;<br /> const 부호 없는 short TYPE_DASH;<br /> const 부호 없는 short TYPE_CUSTOM;<br /> const 부호 없는 short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>인터페이스 MediaResource {<br /> attribute DomString url;<br /> attribute DomString 형식;<br /> 속성 개체 메타데이터;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( 이중 위치);<br /> void play();<br /> void pause();<br /> void seek( 이중 위치);<br /> void seekToLocal( 이중 위치);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaPlayerItem item 항목);<br /> void replaceCurrentResource(MediaResource 리소스, <br /> MediaPlayerItemConfig); <br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> <br /> readonly 속성 TimeRange playbackRange;<br /> 읽기 전용 특성 TimeRange seeableRange;<br /> readonly 속성 double currentTime;<br /> readonly 속성 double localTime;<br /> readonly 속성 TimeRange bufferedRange;<br /> 읽기 전용 속성 DRMManager drmManager;<br /> readonly 속성 MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> <br /> const 부호 없는 short PLAYER_STATUS_INITIALIZED;<br /> const 부호 없는 short PLAYER_STATUS_PREPARING;<br /> const 부호 없는 short PLAYER_STATUS_PREPARED;<br /> const 부호 없는 short PLAYER_STATUS_PLAYING;<br /> const 부호 없는 short PLAYER_STATUS_PAUSED;<br /> const 부호 없는 short PLAYER_STATUS_SEEING;<br /> const 부호 없는 short PLAYER_STATUS_COMPLETE;<br /> const 부호 없는 short PLAYER_STATUS_ERROR;<br /> const 부호 없는 short PLAYER_STATUS_RELEASED;<br /> <br /> 읽기 전용 특성 부호 없는 짧은 상태;<br /> <br /> 특성 부호 없는 짧은 볼륨;<br /> 속성 ABRControlParameters abrControlParameters;<br /> 속성 BufferControlParameters bufferControlParameters;<br /> <br /> const 부호 없는 short VISIBLE; //CC 가시성<br /> const 부호 없는 short INVISIBLE; //CC 가시성<br /> 특성 부호 없는 짧은 가시성;<br /> 특성 TextFormat ccStyle;<br /> 읽기 전용 속성 PlaybackMetrics playbackMetrics;<br /> <br /> 속성 이중 비율;<br /> attribute MediaPlayerView 뷰;<br /> 읽기 전용 속성 타임라인;<br /> 특성 double currentTimeUpdateInterval; <br /> // 이 설정을 설정하면 2.0에 대해 지원되지 않습니다.<br /> };</p> </td> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( int 위치);<br /> void play();<br /> void pause();<br /> void seek( int 위치);<br /> void seekToLocalTime( int 위치);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> readonly 속성 TimeRange playbackRange;<br /> 읽기 전용 특성 TimeRange seeableRange;<br /> readonly 속성 double currentTime;<br /> readonly 속성 double localTime;<br /> readonly 속성 TimeRange bufferedRange;<br /> 읽기 전용 속성 DRMManager drmManager;<br /> readonly 속성 MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const 부호 없는 short PLAYER_STATE_IDLE;<br /> const 부호 없는 short PLAYER_STATE_INITIALIZING;<br /> const 부호 없는 short PLAYER_STATE_INITIALIZED;<br /> const 부호 없는 short PLAYER_STATE_PREPARING;<br /> const 부호 없는 short PLAYER_STATE_PREPARED;<br /> const 부호 없는 short PLAYER_STATE_PLAYING;<br /> const 부호 없는 short PLAYER_STATE_PAUSED;<br /> const 부호 없는 short PLAYER_STATE_SEEING;<br /> const 부호 없는 short PLAYER_STATE_COMPLETE;<br /> const 부호 없는 short PLAYER_STATE_ERROR;<br /> const 부호 없는 short PLAYER_STATE_RELEASED;<br /> const 부호 없는 short PLAYER_STATUS_SUSPENDED;<br /> 읽기 전용 특성 부호 없는 짧은 상태;<br /> <br /> 특성 부호 없는 짧은 볼륨;<br /> 속성 ABRControlParameters abrControlParameters;<br /> 속성 BufferControlParameters bufferControlParameters;<br /> <br /> 읽기 전용 부호 없는 짧은 VISIBLE; //CC 가시성<br /> 읽기 전용 부호 없는 짧은 INVISIBLE; //CC 가시성<br /> 특성 부호 없는 짧은 가시성;<br /> 특성 TextFormat ccStyle;<br /> 읽기 전용 속성 PlaybackMetrics playbackMetrics;<br /> 특성 MediaPlayerConfig mediaPlayerConfig;<br /> 속성 이중 비율;<br /> attribute MediaPlayerView 뷰;<br /> 읽기 전용 속성 타임라인;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const 부호 없는 short PLAYER_STATUS_IDLE;<br /> const 부호 없는 short PLAYER_STATUS_INITIALIZING;<br /> const 부호 없는 short PLAYER_STATUS_INITIALIZED;<br /> const 부호 없는 short PLAYER_STATUS_PREPARING;<br /> const 부호 없는 short PLAYER_STATUS_PREPARED;<br /> const 부호 없는 short PLAYER_STATUS_PLAYING;<br /> const 부호 없는 short PLAYER_STATUS_PAUSED;<br /> const 부호 없는 short PLAYER_STATUS_SEEING;<br /> const 부호 없는 short PLAYER_STATUS_COMPLETE;<br /> const 부호 없는 short PLAYER_STATUS_ERROR;<br /> const 부호 없는 short PLAYER_STATUS_RELEASED;<br /> const 부호 없는 short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>(2.0의 새로운 기능)</td> 
  </tr> 
 </tbody> 
</table>

#### MediaPlayer에서 지원하는 이벤트 {#events-supported-by-mediaplayer}

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
   <td><p>항목이 업데이트됨</p> <p>미디어 플레이어 항목이 업데이트되는 경우.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>업데이트됨</p> <p>미디어 플레이어가 미디어를 성공적으로 업데이트한 경우.</p> </td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetaEvent</td> 
   <td> </td> 
   <td>TtedMetadata</td> 
   <td>TimedMetaEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdated</td> 
   <td>이벤트</td> 
   <td> </td> 
   <td>TmelineUpdated</td> 
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
   <td>2.0용으로 삭제됨</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>이벤트</td> 
  </tr> 
  <tr> 
   <td>상태 변경됨</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>상태 변경됨</td> 
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
   <td>광고 브레이크 이벤트</td> 
   <td> </td> 
   <td>adBreakstart</td> 
   <td>광고 브레이크 이벤트</td> 
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
   <td>광고 진행 이벤트</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>광고 진행 이벤트</td> 
  </tr> 
  <tr> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakComplete</td> 
   <td>광고 브레이크 이벤트</td> 
   <td> </td> 
   <td>adBreakcomplete</td> 
   <td>광고 브레이크 이벤트</td> 
  </tr> 
  <tr> 
   <td>시간 변경됨</td> 
   <td>TimeEvent</td> 
   <td> </td> 
   <td>진행 상황</td> 
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
   <td>seekStart</td> 
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
   <td>예약 도달</td> 
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
   <td>BitrateChangeEvent</td> 
  </tr> 
  <tr> 
   <td>선택한 비율</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>선택한 비율</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>재생 속도</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>재생 속도</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakSkip</td> 
   <td>광고 브레이크 이벤트</td> 
   <td> </td> 
   <td>adBreakSkip</td> 
   <td>광고 브레이크 이벤트</td> 
  </tr> 
  <tr> 
   <td>ad클릭됨<br /> 사용자가 광고를 클릭할 때입니다.</td> 
   <td>AdClickEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>프로필 변경됨<br /> 재생 프로필이 변경되는 때입니다.</td> 
   <td>프로필 이벤트</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> 내부 또는 외부 규칙으로 인해 찾기 위치가 조정되는 경우.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> 미디어 플레이어 항목이 업데이트되는 경우. 재생 시에만 감지할 수 있는 오디오 트랙이 포함된 특정 스트림의 경우, 이 이벤트는 새 오디오 트랙을 사용할 수 있을 때 실행됩니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>캡션 업데이트됨 <br /> 미디어 플레이어 항목이 업데이트되는 경우. 라이브/선형 스트림의 경우 클라이언트는 미디어 리소스를 주기적으로 새로 고쳐 사용 가능한 새로운 콘텐츠를 감지해야 합니다. 이 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> 미디어 플레이어 항목이 업데이트되는 경우. 라이브/선형 스트림의 경우 클라이언트는 미디어 리소스를 주기적으로 새로 고쳐 사용 가능한 새로운 콘텐츠를 감지해야 합니다. 이 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdate<br /> 미디어 플레이어 항목이 업데이트되는 경우. 라이브/선형 스트림의 경우 클라이언트는 미디어 리소스를 주기적으로 새로 고쳐 사용 가능한 새로운 콘텐츠를 감지해야 합니다. 이 경우 특정 미디어 특성이 변경될 수 있습니다.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0의 새로운 기능</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> 시간 이벤트가 생성되면 전송됩니다.</td> 
   <td>Timedevent</td> 
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
   <td><p>인터페이스 ABRControlParameters<br /> {<br /> const 부호 없는 short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const 부호 없는 short ABR_POLICY_MODERATE = 1 ;<br /> const 부호 없는 짧은 ABR_POLICY_AGGREGATIVE = 2 ;<br /> <br /> 특성 부호 없는 짧은 abrPolicy;<br /> 특성 부호 없는 int initialBitRate;<br /> 특성 부호 없는 intBitRate;<br /> 특성 부호 없는 int maxBitRate;<br /> const 부호 없는 short DEFAULT_ABR_INITIAL_BITRATE;<br /> const 부호 없는 short DEFAULT_ABR_MIN_BITRATE;<br /> const 부호 없는 short DEFAULT_ABR_MAX_BITRATE;<br /> 정책 DEFAULT_ABR_POLICY 제약<br /> };</p> </td> 
   <td><p>인터페이스 ABRControlParameters<br /> {<br /> const 부호 없는 short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const 부호 없는 short ABR_POLICY_MODERATE = 1 ;<br /> const 부호 없는 짧은 ABR_POLICY_AGGREGATIVE = 2 ;<br /> <br /> 특성 부호 없는 짧은 abrPolicy;<br /> 특성 부호 없는 int initialBitRate;<br /> 특성 부호 없는 intBitRate;<br /> 특성 부호 없는 int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 버퍼 제어 매개변수 {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> const DEFAULT_INITIAL_BUFFER_TIME;<br /> const DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>인터페이스 BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 텍스트 형식 {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 텍스트 형식<br /> {<br /> // 색상<br /> const 부호 없는 short COLOR_DEFAULT = 0 ;<br /> const 부호 없는 short COLOR_BLACK = 1 ;<br /> const 부호 없는 short COLOR_GRAY = 2 ;<br /> const 부호 없는 short COLOR_WHITE = 3 ;<br /> const 부호 없는 short COLOR_BRIGHT_WHITE = 4 ;<br /> const 부호 없는 short COLOR_DARK_RED = 5 ;<br /> const 부호 없는 short COLOR_RED = 6 ;<br /> const 부호 없는 short COLOR_BRIGHT_RED = 7 ;<br /> const 부호 없는 short COLOR_DARK_GREEN = 8 ;<br /> const 부호 없는 short COLOR_GREEN = 9 ;<br /> const 부호 없는 short COLOR_BRIGHT_GREEN = 10 ;<br /> const 부호 없는 short COLOR_DARK_BLUE = 11 ;<br /> const 부호 없는 short COLOR_BLUE = 12 ;<br /> const 부호 없는 short COLOR_BRIGHT_BLUE = 13 ;<br /> const 부호 없는 short COLOR_DARK_YELLOW = 14 ;<br /> const 부호 없는 short COLOR_YELLOW = 15 ;<br /> const 부호 없는 short COLOR_BRIGHT_YELLOW = 16 ;<br /> const 부호 없는 short COLOR_DARK_MAGENTA = 17 ;<br /> const 부호 없는 짧은 COLOR_MAGENTA = 18 ;<br /> const 부호 없는 short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const 부호 없는 short COLOR_DARK_CYAN = 20 ;<br /> const 부호 없는 short COLOR_CYAN = 21 ;<br /> const 부호 없는 short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> readonly 특성 부호 없는 short fontColor;<br /> readonly 특성 부호 없는 short backgroundColor;<br /> 읽기 전용 특성 부호 없는 짧은 fillColor;<br /> readonly 특성 부호 없는 short edgeColor;<br /> <br /> // 크기<br /> const 부호 없는 short SIZE_DEFAULT = 0 ;<br /> const 부호 없는 short SIZE_SMALL = 1 ;<br /> const 부호 없는 short SIZE_MEDIUM = 2 ;<br /> const 부호 없는 short SIZE_LARGE = 3 ;<br /> <br /> 읽기 전용 특성 부호 없는 짧은 크기;<br /> <br /> // 글꼴<br /> const 부호 없는 short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const 부호 없는 short FONT_EDGE_RAISED = 2 ;<br /> const 부호 없는 short FONT_EDGE_DEDENSED = 3 ;<br /> const 부호 없는 short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> readonly 특성 unsigned short fontEdge;<br /> <br /> // 글꼴<br /> const 부호 없는 short FONT_DEFAULT = 0 ;<br /> const 부호 없는 short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const 부호 없는 short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const 부호 없는 short FONT_CASUAL = 4 ;<br /> const 부호 없는 short FONT_CURSIVE = 5 ;<br /> const 부호 없는 short FONT_SMALL_CAPITALS = 6 ;<br /> 읽기 전용 특성 부호 없는 짧은 글꼴;<br /> readonly 특성 부호 없는 short fontOpacity;<br /> readonly 특성 부호 없는 short backgroundOpacity;<br /> 읽기 전용 특성 부호 없는 짧은 fillOpacity;<br /> 읽기 전용 특성 부호 없는 short DEFAULT_OPACITY;<br /> };</p> </td> 
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
   <td><p>인터페이스 MediaPlayerItemLoader:<br /> {<br /> 무효 로드(MediaResource 리소스, long resourceId,<br /> ItemLoaderListener 수신기, <br /> MediaPlayerItemConfig) ;<br /> void cancel();<br /> readonly 속성 MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
  <tr> 
   <td><p>ItemLoaderListener 인터페이스<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 미디어 특성 API 요소 변경 사항 {#media-characteristics-api-element-changes-for}

이 표에서는 버전 1.3과 2.0 간의 C++ TVSDK에 대한 미디어 특성 API 요소를 비교합니다.

이 항목의 표:

* MediaPlayerItem
* 트랙, 오디오 트랙, 폐쇄 캡션 트랙
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
   <td><p>인터페이스 MediaPlayerItem {<br /> 읽기 전용 속성 MediaResource 리소스;<br /> 읽기 전용 속성 long resourceId;<br /> 읽기 전용 속성 부울 라이브;<br /> <br /> 읽기 전용 속성 부울 hasAlternateAudio;<br /> readonly 속성 AudioTrackList audioTracks;<br /> readonly 속성 AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack); <br /> <br /> 읽기 전용 속성 부울 hasClosedCaptions;<br /> readonly 속성 ClosedCaptionsTrackList closedCaptionsTracks;<br /> 읽기 전용 특성 ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack); <br /> <br /> 읽기 전용 속성 부울 hasTimedMetadata;<br /> readonly 속성 TimedMetadataList timedMetadata;<br /> 읽기 전용 속성 부울 다이내믹;<br /> <br /> 읽기 전용 속성 부울 isProtected;<br /> 읽기 전용 속성 DRMMetadataInfoList drmMetadataInfos;<br /> 읽기 전용 속성 ProfileList 프로필;<br /> 읽기 전용 속성 프로필 selectedProfile;<br /> <br /> 읽기 전용 속성 부울 trickPlaySupported;<br /> 읽기 전용 속성 FloatArray availablePlaybackRates;<br /> 읽기 전용 속성 float selectedPlaybackRate;<br /> <br /> <br /> readonly 속성 MediaPlayer mediaPlayer;<br /> readonly 특성 MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>인터페이스 MediaPlayerItem {<br /> 읽기 전용 속성 MediaResource 리소스;<br /> 읽기 전용 속성 long resourceId;<br /> 읽기 전용 속성 부울 라이브;<br /> <br /> 읽기 전용 속성 부울 hasAlternateAudio;<br /> readonly 속성 AudioTrackList audioTracks;<br /> attribute AudioTrack selectedAudioTrack;<br /> <br /> <br /> 읽기 전용 속성 부울 hasClosedCaptions;<br /> readonly 속성 ClosedCaptionsTrackList ccTracks;<br /> 특성 ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> 읽기 전용 속성 부울 hasTimedMetadata;<br /> readonly 속성 TimedMetadataList timedMetadata;<br /> 읽기 전용 속성 부울 다이내믹;<br /> <br /> 읽기 전용 속성 부울 isProtected;<br /> 읽기 전용 속성 DRMMetadataInfoList drmMetadataInfos;<br /> 읽기 전용 속성 ProfileList 프로필;<br /> <br /> <br /> 읽기 전용 속성 부울 trickPlaySupported;<br /> readonly 속성 Int32Array availablePlaybackRates;<br /> <br /> readonly 속성 StringList adTags;<br /> <br /> readonly 속성 MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 추적/AudioTrack/ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>인터페이스 추적<br /> {<br /> 읽기 전용 속성 DomString 이름;<br /> 읽기 전용 특성 DomString 언어;<br /> 읽기 전용 속성 부울 기본값;<br /> 읽기 전용 속성 부울 autoSelect;<br /> }; </p> </td> 
   <td>2.0의 새로운 기능</td> 
  </tr> 
  <tr> 
   <td><p>인터페이스 AudioTrack : 추적<br /> {<br /> 읽기 전용 속성 DomString 이름; //FromTrack<br /> readonly 속성 DomString 언어;//FromTrack<br /> 읽기 전용 속성 부울 기본값; // 추적에서<br /> 읽기 전용 속성 부울 autoSelect;//FromTrack<br /> <br /> 읽기 전용 특성 부호 없는 int pid;<br /> };</p> </td> 
   <td><p>인터페이스 AudioTrack<br /> {<br /> 읽기 전용 속성 DomString 이름;<br /> 읽기 전용 특성 DomString 언어; <br /> 읽기 전용 속성 부울 기본값;<br /> 읽기 전용 속성 부울 autoSelect;<br /> 읽기 전용 속성 부울 강제 적용;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 AudioTrackList<br /> {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter AudioTrack(부호 없는 긴 색인);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>인터페이스 ClosedCaptionsTrack : 추적<br /> {<br /> 읽기 전용 속성 DomString 이름; //FromTrack<br /> readonly 속성 DomString 언어;//FromTrack<br /> 읽기 전용 속성 부울 기본값; // FromTrack<br /> 읽기 전용 속성 부울 autoSelect;//FromTrack<br /> <br /> <br /> const 부호 없는 short SERVICE_608_CAPTIONS = 0;<br /> const 부호 없는 short SERVICE_708_CAPTIONS = 1;<br /> const 부호 없는 short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> readonly 특성 부호 없는 short serviceType;<br /> 읽기 전용 속성 부울 강제 적용;<br /> };</p> </td> 
   <td><p>인터페이스 ClosedCaptionsTrack<br /> {<br /> 읽기 전용 속성 DomString 이름;<br /> 읽기 전용 특성 DomString 언어;<br /> 읽기 전용 속성 부울 기본값;<br /> <br /> <br /> 읽기 전용 속성 부울 활성화;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 ClosedCaptionsTrackList<br /> {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter ClosedCaptionsTrack(부호 없는 긴 색인);<br /> };</p> </td> 
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
   <td>프로필: 2.0에 대한 변경 사항 없음</td> 
   <td><p>인터페이스 프로필<br /> {<br /> 읽기 전용 특성 부호 없는 int 너비;<br /> 읽기 전용 특성 부호 없는 int 높이;<br /> 읽기 전용 특성 부호 없는 int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: 2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 프로필 목록<br /> {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter 프로필(부호 없는 긴 색인);<br /> };</p> </td> 
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
   <td><strong>DRMMetadataInfo</strong>: 2.0에 대한 변경 사항 없음</td> 
   <td><p>인터페이스 DRMMetadataInfo<br /> { <br /> 읽기 전용 속성 DRMMetadata 메타데이터;<br /> 읽기 전용 속성 long prefetchTimestamp;<br /> readonly 속성 TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: 2.0에 대한 변경 사항 없음</td> 
   <td><p>인터페이스 DRMMetadataInfoList<br /> {<br /> 읽기 전용 특성 부호 없는 긴 길이;<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## C++ 오류를 다른 언어로 예외에 매핑 {#mapping-c-errors-to-exceptions-in-different-languages}

C++ 오류 코드를 다른 언어의 예외에 매핑할 수 있습니다.

C++ PSDK에는 API에 대한 &quot;No Throw&quot; 정책이 있습니다. 대부분의 API 메서드는 메서드가 성공적으로 실행되었는지 여부를 나타내는 PSDKErrorCode 값을 반환합니다. 비동기 오류는 오류 이벤트를 통해 통지됩니다.

ActionScript 및 JAVA PSDK에는 다른 정책이 있습니다. 대부분의 오류는 메서드의 동기 부분을 실행할 수 없음을 나타내기 위해 ArgumentError 또는 IllegalStateException을 발생시킵니다. 이러한 예외는 발생하지 않으며, 예외 처리를 위해 애플리케이션 코드가 책임집니다. 일반적으로 메서드 호출이 실패한 이유에 대한 유용한 정보를 전달합니다. 예를들어, prepareToPlay 명령이 잘못된 상태에서 호출되면 다음 예외가 throw됩니다.

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

또한 ActionScript/JAVA는 생성자에서 예외를 throw하여 일부 내부 개체가 잘못 생성되었음을 나타냅니다. 이러한 예외는 내부적으로 처리되며 애플리케이션에 전파되지 않습니다. 예외는 애플리케이션에 전송되는 경고 알림에 포함됩니다

예를 들어 수신된 광고 응답에 유효한 미디어 파일이 없는 경우 유효한 광고 자산 개체 또는 광고를 만들 수 없습니다. 따라서 타임라인에 광고가 배치되지 않고 NotificationEvent.OperationFailed 알림이 발송됩니다.

AVE(Adobe 비디오 엔진)에서 비동기적으로 수신된 오류 또는 경고 코드는 일반 이벤트로 애플리케이션에 발송됩니다. 알림 이벤트에는 수신된 모든 오류 코드와 URL, 리소스 식별자, 핸들 등과 같은 추가 메타데이터가 포함됩니다. 오류가 심각하고 현재 미디어 재생을 계속할 수 없는 경우 MediaPlayer가 ERROR 상태로 전환되고 onStatusChanged 콜백 또는 MediaPlayerStatusChanged.STATUS_CHANGED 이벤트가 전달됩니다. 재생이 계속될 수 있으면 일반 알림 이벤트가 발송됩니다.

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
   <td>예외 코드 = 1, 설명 = "INVALID_ARGUMENT" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>예외 코드 = 2, 설명 = "GENERIC_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>ECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>예외 코드 = 3, 설명 = "ILLEGAL_STATE" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>ECIinterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 4, 설명 = "GENERIC_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 5, 설명 = "CREATION_FAILED" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 5, 설명 = "CREATION_FAILED" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 7, 설명 = "DATA_NOT_AVAILABLE" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>ECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 8, 설명 = "SEEK_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 9, 설명 = "UNSUPPORTED_FEATURE" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 10, 설명 = "RANGE_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 11, 설명 = "CODEC_NOT_SUPPORTED" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 12, 설명 = "MEDIA_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 13, 설명 = "NETWORK_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error 또는 MediaPlayerNotification.Warning</td> 
   <td>MediaError 또는 NotificationEvent</td> 
   <td>예외 코드 = 14, 설명 = "GENERIC_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 15, 설명 = "INVALID_SEEK_TIME" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 16, 설명 = "AUDIO_TRACK_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>다른 액세스<p>스레드 오류</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 17, 설명 = "GENERIC_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 18, 설명 = "GENERIC_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 19, 설명 = "GENERIC_ERROR" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>예외 코드 = 200, 설명 = "PLAYBACK_OPERATION_FAILED" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNactiveWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>예외 코드 = 201, 설명 = "NATIVE_WARNING" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>예외 코드 = 202, 설명 = "AD_RESOLVER_FAILED" 및 additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0에 대한 유틸리티 및 도우미 API 요소 변경 사항 {#utility-and-helper-api-element-changes-for}

이 표에서는 버전 1.3과 2.0 간의 JavaScript TVSDK에 대한 유틸리티 및 도우미 API 요소를 비교합니다.

이 항목의 표:

* 버전
* TimeRange
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
   <td><p>인터페이스 버전<br /> {<br /> 읽기 전용 특성 DomString 버전;<br /> 읽기 전용 속성 DomString 설명;<br /> 읽기 전용 속성 long major;<br /> 읽기 전용 속성 long minor;<br /> 읽기 전용 속성이 긴 버전입니다.<br /> readonly 특성 long apiVersion;<br /> };</p> </td> 
   <td><p>인터페이스 버전<br /> {<br /> 읽기 전용 특성 DomString 버전;<br /> 읽기 전용 속성 DomString 설명;<br /> 읽기 전용 특성 DomString 주;<br /> 읽기 전용 특성 DomString 부;<br /> 읽기 전용 특성 DomString 수정 버전,<br /> 읽기 전용 속성 DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 TimeRange<br /> {<br /> 읽기 전용 특성 부호 없는 long begin;<br /> 읽기 전용 특성 부호 없는 긴 끝;<br /> 읽기 전용 특성 부호 없는 긴 기간;<br /> };</p> </td> 
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
   <td>2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer);<br /> distachMediaPlayer();<br /> <br /> 읽기 전용 속성 DeviceInformation deviceInformation;<br /> 읽기 전용 속성 PlaybackInformation playbackInformation;<br /> };</p> </td> 
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
   <td><p>인터페이스 장치 정보<br /> {<br /> 읽기 전용 속성 DomString os;<br /> <br /> <br /> <br /> 읽기 전용 속성 DomString id;<br /> 읽기 전용 속성 int densityDPI;<br /> readonly 속성 int heightPixels;<br /> readonly 속성 int widthPixels;<br /> readonly 속성 부울 seekToKeyFrame;<br /> };</p> </td> 
   <td><p>인터페이스 장치 정보<br /> {<br /> 읽기 전용 속성 DomString os;<br /> readonly 속성 int sdk;<br /> 읽기 전용 특성 DomString 모델;<br /> readonly 속성 DomString 제조업체;<br /> 읽기 전용 속성 DomString id;<br /> 읽기 전용 속성 int densityDPI;<br /> readonly 속성 int heightPixels;<br /> readonly 속성 int widthPixels;<br /> <br /> };</p> </td> 
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
   <td>2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 LoadInfo<br /> {<br /> 읽기 전용 속성 DomString url;<br /> 읽기 전용 속성 int 크기;<br /> 읽기 전용 속성 double downloadDuration;<br /> readonly 속성 int periodIndex;<br /> readonly 특성 double mediaDuration;<br /> readonly 속성 short TRACK_TYPE_FRAGMENT;<br /> readonly 속성 short TRACK_TYPE_TRACK;<br /> readonly 특성 short TRACK_TYPE_MANIFEST;<br /> readonly 특성 short type;<br /> readonly 속성 DomString trackName;<br /> readonly 속성 DomString trackType;<br /> readonly 속성 int trackIndex;<br /> };</p> </td> 
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
   <td>2.0에 대한 변경 내용 없음</td> 
   <td><p>인터페이스 보기<br /> {<br /> 읽기 전용 특성 부호 없는 짧은 x;<br /> 읽기 전용 특성 부호 없는 짧은 y;<br /> 읽기 전용 특성 부호 없는 짧은 너비;<br /> 읽기 전용 특성 부호 없는 짧은 높이;<br /> <br /> void setSize(부호 없는 짧은 너비, 부호 없는 짧은 높이);<br /> void setPos(부호 없는 짧은 x, 부호 없는 짧은 y);<br /> }</p> </td> 
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
   <td><p>인터페이스 PlaybackInformation<br /> {<br /> readonly 속성 double timeToFirstByte;<br /> readonly 속성 double timeToLoad;<br /> readonly 속성 double timeToStart;<br /> readonly 속성 double timeToFail;<br /> readonly 속성 int totalSecondsPlayed;<br /> readonly 속성 int totalSecondsSpent;<br /> readonly 속성 double frameRate;<br /> readonly 속성 int droppedFrameCount;<br /> 읽기 전용 속성 int recognizedBandwidth;<br /> readonly 속성 int bitrate;<br /> readonly 속성 double bufferTime;<br /> readonly 속성 int bufferLength;<br /> readonly 속성 int emptyBufferCount;<br /> readonly 특성 double bufferingTime;<br /> };</p> </td> 
   <td><p>인터페이스 PlaybackInformation<br /> {<br /> readonly 속성 double timeToFirstByte;<br /> readonly 속성 double timeToLoad;<br /> readonly 속성 double timeToStart;<br /> readonly 속성 double timeToFail;<br /> readonly 속성 int totalSecondsPlayed;<br /> readonly 속성 int totalSecondsSpent;<br /> readonly 속성 double frameRate;<br /> readonly 속성 int droppedFrameCount;<br /> <br /> readonly 속성 int bitrate;<br /> readonly 속성 double bufferTime;<br /> readonly 속성 int bufferLength;<br /> readonly 속성 int emptyBufferCount;<br /> readonly 특성 double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
