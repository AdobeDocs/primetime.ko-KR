---
title: Android용 TVSDK 1.4 - 2.5(Java)
seo-title: Android용 TVSDK 1.4 - 2.5(Java)
description: TVSDK 2.5는 성능, 보안, 통합 향상 등의 측면에서 버전 1.4보다 다양한 이점을 제공합니다.
seo-description: TVSDK 2.5는 성능, 보안, 통합 향상 등의 측면에서 버전 1.4보다 다양한 이점을 제공합니다.
uuid: aaab7aec-cb5b-4840-82e8-7112a8d98a8a
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: 8d9136bf-b3ae-450c-bd8a-0bb246527886
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Android용 TVSDK 1.4 - 2.5(Java) {#tvsdk-to-for-android-java}

TVSDK 2.5는 성능, 보안, 통합 향상 등의 측면에서 버전 1.4보다 다양한 이점을 제공합니다.

TVSDK는 디바이스에서 가장 중요한 문제를 해결합니다. Android는 시장 점유율의 86% 이상을 차지하며, 이것이 계속 전 세계적으로 우세합니다. Android에서 TVSDK로 마이그레이션하면 재생 성능을 최적화하여 사용자 참여도를 높이고 새로운 컨텐츠 포맷에 대한 지원을 통해 출시 시간을 단축할 수 있습니다.

## TVSDK v2.5로 마이그레이션하여 얻을 수 있는 이점 {#benefits-of-migrating-to-tvsdk-v}

TVSDK 2.5는 성능, 보안, 통합 향상 등의 측면에서 버전 1.4보다 다양한 이점을 제공합니다. 이 새로운 버전으로 마이그레이션하여 얻을 수 있는 이점에 대해 자세히 살펴보십시오.

타사 벤치마크 조사 결과에 따르면 v2.5는 시작 시간의 5배 감소 및 업계 평균에 비해 드롭된 프레임의 3.8배 감소 기능을 제공합니다.

| 성능 기능 | 설명 |
|--- |--- |
| VOD 및 라이브용 인스턴트 온 | TV와 같은 경험을 위해 채널 전환 시 VOD 및 실시간 선형 스트리밍에 대한 즉각적인 재생을 위해 선분을 미리 로드할 수 있습니다. |
| 레이지 광고 로딩 | 병렬 스레드에서 미드롤 광고를 확인하는 동안 프리롤 또는 컨텐츠를 사용할 수 있게 되면 재생을 시작합니다. |
| 지속적인 네트워크 연결 | 네트워킹 코드의 효율성을 높이고 지연 시간을 줄임으로써 재생 성능을 향상시킵니다. |
| 향상된 ABR 로직 | 새로운 ABR 로직은 버퍼 길이, 버퍼 길이 변경 속도 및 측정된 대역폭을 기반으로 합니다. 따라서 ABR은 대역폭 변동 시 올바른 비트 전송률을 선택하고 버퍼 길이 변경되는 속도를 모니터링하여 비트율 전환이 실제로 발생하는 횟수를 최적화합니다. |
| 부분 세그먼트 다운로드 | 클라이언트 쪽에서 비디오를 안전하게 렌더링하기 위해 세그먼트의 프레임을 사용할 수 있게 되면 바로 재생을 시작합니다. |
| 병렬 다운로드 | TVSDK는 오디오 및 비디오 세그먼트를 동시에 다운로드하여 향상된 컨텐츠를 제공하여 재생 성능을 최적화합니다. |

재생 기능은 디지털 기반의 리니어 브로드캐스트의 경험을 제공하여 소비자의 참여를 높일 수 있습니다. 또한 HD 재생을 위한 Widevine과 같은 기본 DRM을 활용할 수 있습니다.

| 재생 기능 | 설명 |
|--- |--- |
| MP4 재생 | TVSDK 내에서 재생하기 위해 MP4 단편 클립을 다시 코딩할 필요가 없습니다. |
| DASH VOD 컨텐츠 재생 | 기본 DASH VOD 재생 사용 사례가 지원됩니다. |
| ABR을 사용한 부드러운 트릭플레이 | 낮은 속도의 키프레임과 빠른 속도로 I-Frame을 사용하여 HLS에서 빨리 감기 및 되감기 기능을 지원합니다. 지원되는 모든 프레임에 대한 ABR 지원 |

이 기능은 기본 DRM을 통한 HD 재생과 같은 스튜디오 제한 사항을 충족하기 위해 중요합니다.

| 기능 | 설명 |
|--- |--- |
| 해상도 기반 출력 보호 | drm 요구 사항에 따라 허용되는 특정 해상도로만 재생을 제한할 수 있습니다. Primetime DRM을 통해서만 제공 |
| 무선 지원 | 기본 DRM 사용 사례를 활성화하는 DASH VOD 스트림에서 지원됩니다. |

직접 비용 청구를 향상해도 매월 청구 수동 보고서를 작성할 필요가 없습니다. VHL 2.0을 사용하면 사전 빌드 통합과 추적 정확성을 통해 출시 시간을 단축할 수 있습니다.

| 기능 | 설명 |
|--- |--- |
| 해자 통합 | 해자에서 광고 보기 측정 지원 |
| VHL 2.0 | Adobe Analytics에 대한 사용 데이터 자동 수집을 위해 최적화된 최신 비디오 하트비트 라이브러리 통합 |
| 장애 조치 지원 | 호스트 서버, 재생 목록 파일 및 세그먼트에 장애가 발생하더라도 중단 없이 계속 재생할 수 있는 추가 전략이 구현되었습니다. |
| 직접 청구 통합 | 고객이 사용하는 스트림에 대해 Adobe Primetime에서 인증한 Adobe Analytics 백엔드로 청구 지표를 전송합니다. |

>[!NOTE]
>
>다중 CDN 지원을 제외한 TVSDK v1.4의 모든 기능이 v2.5에서 지원됩니다.

## 마이그레이션 프로세스 개요 {#overview-of-the-migration-process}

TVSDK 1.4에서 2.5로 원활하게 마이그레이션하려면 버전 2.5 라이브러리로 변경하고 다시 컴파일한 다음 이 문서를 사용하여 발생하는 문제를 디버깅합니다.

TVSDK v1.4 라이브러리는 v2.5 라이브러리와 함께 작동하지 않고 함께 공존합니다. TVSDK 2.5와 함께 v2.5 라이브러리를 사용하고 애플리케이션과 통합을 마이그레이션하여 TVSDK 2.5로 업그레이드해야 합니다.이 문서에서는 애플리케이션 코드의 변경 방법 및 내용과 다시 컴파일하는 동안 오류를 해결하는 방법에 대해 설명합니다.

psdk.jar 파일은 다른 기능을 지원하기 위해 타사 라이브러리를 사용합니다. 라이브러리의 제거를 방지하려면 `proguard.cfg` 파일에 다음을 포함합니다.

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

TVSDK 기반 JAR 파일을 포함하려면 `build.gradle` 파일에 compile 지시문을 포함해야 합니다. 앱에 Adobe Video Analytics가 포함되어 있는 경우 앱의 Adobe Video Analytics 통합에 필요한 추가 병에 대한 컴파일 지시문을 포함해야 합니다

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

이 문서에서는 사소한 여러 변경 사항이 적용되지 않습니다. API의 사소한 변경 사항은 Android Java [API용 TVSDK 2.5를 참조하십시오](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html). 해당 C++ API 참조에는 자세한 설명이 있습니다. 유사한 C++ API 문서는 Android C+ [API용 TVSDK 2.5를 참조하십시오](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html).

API 사용의 여러 예는 TVSDK로 배포되는 참조 구현에서 다룹니다.

## TVSDK v2.5의 API 변경 사항 {#api-changes-in-tvsdk-v}

새로운 API, 오래된 API 및 수정된 API는 아래에 설명되어 있습니다.

| TVSDK v1.4 | TVSDK v2.5 | 설명 |
|--- |--- |--- |
| import com.adobe.ave.drm.DRMAcquireLicenseSettings | import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; | TVSDK 2.5 API의 모든 클래스 이름은 com.adobe.mediacore 접두사로 시작합니다. 이것은 단지 한 예일 뿐이다. |
| MediaPlayerException, IllegalStateException 또는 IllegalArgumentException | MediaPlayerException | 2.5에서 API는 MediaPlayerException만 생성합니다. |
| MediaPlayer.PlayerState(MediaPlayer.Event.PLAYBACK) | MediaPlayerStatus(MediaPlayerEvent.STATUS_CHANGED) | v2.5에서 MediaPlayer.PlayerState가 별도의 열거형 MediaPlayerStatus로 이름이 변경되었습니다. |
| DefaultMediaPlayer.create (getActivity().getApplicationContext()) | MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext(); | 객체를 만드는 데 사용되는 정적 메서드는 공용 생성자로 대체됩니다. |
| MediaPlayer.seekToLocalTime() | MediaPlayer.seekToLocal() | MediaPlayer.seekToLocalTime() 메서드를 이제 MediaPlayer.seekToLocal()이라고 합니다. |
| closedCaptionsTrack.isActive() |  | 사용할 수 없음 |
| MetadataNode | 메타데이터 | v2.5에서 Metadata 클래스는 v1.4 MetadataNode 클래스의 사용을 대체합니다. |
| DefaultMetadataKeys | MetadataKeys | v1.4의 DefaultMetadataKeys는 v2.5 열거형 MetadataKeys에 있습니다. |
| AdvertisingFactory | ContentFactory | v1.4에서 AdvertisingFactory가 v2.5에서 ContentFactory로 이름이 변경되었습니다. |
| PlacementOpportunityDetector | OpportunityGenerator | 탐지기는 생성기로 대체됩니다. |
| mediaPlayer.getView().notifyClick(); | mediaPlayer.notifyClick(); | MediaPlayerView의 notifyClick() 메서드가 MediaPlayer 클래스로 이동되었습니다. |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, int nMaxBitRate) | public ABRControlParameters(int nInitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, int nMaxTrickBitRate, int n MaxTrickPlayBandwidthUsage, double dMaxPlayoutRate) |  |
| playbackInformation.getTimeToFirstFrame() |  | 사용할 수 없음 |
|  | playbackInformation.get IsceptedBandwidth() | TVSDK v2.5 QOSProvider는 스트리밍 세션 동안 인식된 대역폭을 확인하는 새로운 속성을 제공합니다. |

### 제거된 클래스 {#removed-classes}

다음 클래스는 제거되고 이에 상응하는 클래스가 없습니다.

* `TimeRangeCollection`
* `PSDKConfig`
* `BaseLogger`
* `DefaultLogger`
* `Log`
* `Logger`
* `LogFactory`
* `NullLogger`

이러한 클래스 중 마지막 6개는 참조 구현에서 유틸리티 클래스로 사용할 수 있습니다.

## 네임스페이스 변경 {#namespace-changes}

TVSDK 2.5 API는 네임스페이스를 통합합니다.

TVSDK 2.5 API의 모든 클래스 이름은 com.adobe.mediacore 접두사로 시작합니다. TVSDK 1.4 API의 일부 클래스 이름은 com.adobe.ave로 시작합니다. 해당 2.5 클래스는 com.adobe.ave를 com.adobe.mediacore로 변경합니다. 예를 들어 1.4 및 2.5에 대한 다음 코드 줄의 변경 사항을 확인하십시오.

```java
// TVSDK 1.4
import com.adobe.ave.drm.DRMAcquireLicenseSettings; import com.adobe.ave.drm.DRMLicense;
import com.adobe.ave.drm.DRMManager; import com.adobe.ave.drm.DRMMetadata
```

```java
// TVSDK 2.5
import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; import com.adobe.mediacore.drm.DRMLicense;
import com.adobe.mediacore.drm.DRMManager; import com.adobe.mediacore.drm.DRMMetadata;
```

## 이벤트 처리 변경 사항 {#changes-in-event-handling}

이 버전에서 이벤트를 등록하려면 처리기를 에 `addEventListener`전달합니다. 이벤트 목록은 버전 1.4에서 버전 2.5로 대폭 수정되었습니다.\
예를 들어, 다음은 `MediaPlayerEvent.STATUS_CHANGED:`

```java
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,
new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
});
```

이것은 이벤트가 1.4에서 등록된 방식입니다.

```java
mPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {
@Override
public void onStateChanged(MediaPlayer.PlayerState state,
MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});
```

MediaPlayerEvent 열거형에 모든 이벤트 코드가 포함되어 있습니다. 1.4의 다음 이벤트 코드는 더 이상 2.5에 존재하지 않습니다.

* `ADBREAK_PLACEMENT_COMPLETED`
* `ADBREAK_PLACEMENT_FAILED`
* `ADBREAK_REMOVAL_COMPLETED`
* `AD_BREAK_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_FAILED`
* `AUDIO_TRACK_FAILED`
* `BACKGROUND_MANIFEST_FAILED`
* `BUFFERING_FULL, CUSTOM_AD_EVENT`
* `CONTENT_MARKER`
* `CONTENT_PLACEMENT_COMPLETE`
* `CONTENT_CHANGED`
* `ITEM_REPLACED`
* `ITEM_READY`
* `VIEW_CLICKED`
* `PREPARED`
* `UPDATED`
* `OPPORTUNITY_COMPLETED`
* `OPPORTUNITY_CREATED`
* `OPPORTUNITY_FAILED`
* `PAUSE_AT_PERIOD_END`
* `PLAYBACK_STARTED`
* `PLAYBACK_PAUSED`
* `PLAYBACK_COMPLETED`
* `PLAY_COMPLETE`
* `POST_ROLL_COMPLETE`
* `RESOURCE_LOADED`
* `TIMED_METADATA_SKIPPED`
* `VIDEO_ERROR`
* `VIDEO_STATE_CHANGED`

다음 이벤트 코드는 2.5에서 새로 추가되었습니다.

* `AD_RESOLUTION_COMPLETE`
* `BUFFER_PREPARED`
* `CAPTIONS_UPDATED`
* `MANIFEST_UPDATED`
* `PLAYBACK_RANGE_UPDATED`
* `RESERVATION_REACHED`
* `TIME_CHANGED`
* `TIMED_EVENT`
* `TIMED_METADATA_ADDED_IN_BACKGROUND`

### 이름이 변경된 이벤트 {#renamed-events}

| 새 이름 | 이전 이름 |
|--- |--- |
| SEEK_BEGIN | SEEK_STARTED |
| SEEK_END | SEEK_COMPLETED |
| SEEK_POSITION_ADJUTED | SEEK_ADJUST_COMPLETED |
| BUFFERING_BEGIN | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATUS_CHANGED | STATE_CHANGED |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_ADDED |
| SIZE_AVAILABLE | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## MediaPlayer 변경 사항 {#mediaplayer-changes}

몇 가지 방법을 구성하고 변경하는 새로운 `MediaPlayer` 방법입니다.

**MediaPlayer 클래스 변경 사항**

다음은 `MediaPlayer` 클래스의 변경 사항입니다.

* 열거형이 `MediaPlayerStatus` 바뀝니다 `MediaPlayer.PlayerState`. 예:

```java
//TVSDK v1.4
mPlayer. addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {

@Override
public void onStateChanged(MediaPlayer.PlayerState state,MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});

//TVSDK v2.5
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
//Additional handlers.
...
});
```

* 이제 `MediaPlayer.seekToLocalTime()` 메서드가 호출됩니다 `MediaPlayer.seekToLocal`. 예:

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* 이제 `MediaPlayerView.notifyClick()` 방법이 사용됩니다 `MediaPlayer.notifyClick()`. 예:

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* 이전 `MediaPlayer.MediaPlayer.getNotificationHistory()` 방법은 이제 사라지고 바뀌지 않습니다.
* The former `MediaPlayer.replaceCurrentItem()` is split into two methods:한 `replaceCurrentResource()`예로 `MediaResource`들고, `replaceCurrentItem()`한 예로 `MediaPlayerItem`들어보죠. 예:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());

mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5 - replacing a resource
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());
...
try {
mMediaPlayer.replaceCurrentResource(playerResource, _mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
// TVSDK 2.5 - replacing an Item
MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(context, new MediaPlayerItemLoader.LoaderListener() {

@Override
public void onError(PSDKErrorCode psdkErrorCode, String s) {
...
}
@Override
public void onLoadComplete(MediaPlayerItem mediaPlayerItem) {
...
}
@Override
public void onBufferingBegin() {
...
}
@Override
public void onBufferPrepared() {
...
}
});
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());

itemLoader.load(playerResource); itemLoader.prepareBuffer();
mediaPlayer.replaceCurrentItem(itemLoader.getItem());
```

일시 중단의 경우와 마찬가지로 사전 초기화된 MediaPlayer 인스턴스 간을 전환할 수 있습니다.

**생성자가 정적 create() 메서드를 대체합니다.**

TVSDK v1.4의 `create()` 방법을 사용하는 대신 TVSDK v2.5에서 생성자를 사용할 수 있습니다.v2.5에서는 이름이 Default로 시작하는 모든 클래스를 사용할 수 `DefaultMediaPlayer``DefaultNetworkConfig``DefaultContentFactory`없습니다.

경우에 따라 TVSDK v1.4 API는 클래스를 만드는 데 다음 패턴을 사용합니다.

1. 인터페이스(예: `MediaPlayer`)를 정의합니다.
1. 기본 클래스(예: `DefaultMediaPlayer`)를 제공합니다.
1. 인터페이스를 구현하는 클래스를 제공하기 위해 기본 클래스에 메서드를 `create()` 제공합니다.

TVSDK v2.5에서 이러한 인터페이스는 콘크리트 클래스이며 각 생성자를 사용하여 이러한 클래스의 인스턴스를 만듭니다. 다음 코드 조각은 이러한 차이점을 설명합니다.

```java
//TVSDK v1.4
// Create a media player
// MediaPlayer is an interface
private MediaPlayer createMediaPlayer() { MediaPlayer mediaPlayer =
DefaultMediaPlayer.create(getActivity().getApplicationContext()); return mediaPlayer;

//TVSDK v2.5
// Create a media player
// MediaPlayer is a class that you instantiate private MediaPlayer createMediaPlayer() {
MediaPlayer mediaPlayer =
new MediaPlayer(getActivity().getApplicationContext()); return mediaPlayer;
}
```

이 패턴을 따르지 않지만 1.4에서 `create()` 메서드를 사용하는 다른 클래스에는 다음이 포함됩니다.

* MediaResource\
   이전에 사용된 `MediaResource.createFromUrl()`것입니다. 이제 URL, 리소스 유형 및 메타데이터를 가져오는 생성자를 사용합니다. 예:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());
mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, getAdvertisingMetadata());

try { mediaPlayer.replaceCurrentResource(playerResource,_mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
```

* 광고
* AdAsset
* AdBreak

일부 클래스(예: `ContentFactory`)는 공개적으로 사용할 수 있는 기본 구현(예: `DefaultContentFactory`)이 없는 추상 클래스입니다. 이러한 경우 다음과 같은 편의 기능을 통해 기본 구현을 제공할 수 있습니다. `mediaPlayerItemConfig.getDefaultContentFactory()`

**자막 변경**

다음 변경 사항은 자막과 관련된 클래스에 영향을 줍니다.

* 닫힌 캡션 트랙을 검색할 때 활성 트랙만 `MediaPlayerItem.getClosedCaptionTracks()` 반환합니다.
* `ClosedCaptionTrack` 더 이상 `isActive()` 메서드가 없습니다.

```java
//TVSDK v1.4
public List<String> getClosedCaptionTracks(String label) {
List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks(); Iterator<ClosedCaptionsTrack> iterator =
closedCaptionsTracks.iterator();
if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); String isActive = closedCaptionsTrack.isActive() ? " (" + label
+ ")" : "";
closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName()
+ " : " + closedCaptionsTrack.getLanguage() + isActive);
}
}
return closedCaptionsTracksAsStrings;
}

//TVSDK v2.5
public List<String> getClosedCaptionTracks(String label) {

MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks();
Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator();

List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); closedCaptionsTracksAsStrings.
add(closedCaptionsTrack.getName() + " : ");
}
}
return closedCaptionsTracksAsStrings;
}
// Add snippet and desc for CaptionsUpdatedEventListener mediaPlayer.addEventListener(MediaPlayerEvent.CAPTIONS_UPDATED,
captionsUpdatedEventListener);

private final CaptionsUpdatedEventListener captionsUpdatedEventListener = new CaptionsUpdatedEventListener() {

@Override
public void onCaptionsUpdated(MediaPlayerItemEvent mediaPlayerItemEvent) { getActivity().findViewById(R.id.sbPlayerControlCC).setVisibility(
View.VISIBLE/*Visible*/);
}
};
```

## 광고 변경 {#advertising-changes}

버전 2.5에는 몇 가지 광고 관련 변경 사항이 있습니다.

**광고 행동 변경 사항**

사용자가 광고 창을 벗어나는 검색을 수행할 때의 기본 동작은 v2.5에서 약간 변경됩니다.광고 브레이크가 표시되지 않으면 광고가 앞으로 검색 후 재생됩니다. 앱이 기본 광고 정책을 사용하는 경우 재생이 완료된 후 광고 중단이 제거됩니다. TVSDK v2.5를 사용하는 경우 사용자가 타임라인에서 광고 창을 뒤쫓고 광고 브레이크가 표시되지 않으면 광고가 재생되지 않습니다.

그러나 TVSDK v1.4에서는 기본적으로 뒤로 이동 시 광고가 재생됩니다. 예를 들어 세 번째 광고 브레이크와 네 번째 광고 브레이크 사이에서 뒤로 이동하는 경우 TVSDK v1.4의 기본 동작은 세 번째 광고 브레이크를 재생하는 것입니다.

**광고 규칙 변경**

광고 규칙은 JSON 파일을 사용하여 지정됩니다. JSON 파일의 형식은 두 버전의 TVSDK에서 동일하게 유지됩니다. 그러나 TVSDK v2.5에서 광고 규칙 JSON 파일은 HTTP URL을 통해 액세스할 수 있는 위치에 호스팅되어야 합니다. 응용 프로그램은 AuditudeSettings 인스턴스를 사용할 수 있습니다.

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

TVSDK 버전 1.4에서는 이 파일이 애플리케이션의 자산 폴더 아래에 배치되고 TVSDK는 파일을 로드합니다.

**광고 팩토리 이름 바꾸기**

`AdvertisingFactory` 의 이름이 `ContentFactory`변경되었습니다. With `ContentFactory` you can create customized advertising workflows by overriding some of its method. 다음과 같이 기본 동작을 유지하려면 null 반환 옵션을 사용합니다.

```java
//TVSDK v2.5
new ContentFactory() {
@Override
public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item) { return new CustomAdPolicySelector();
}
@Override
public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { return null;
}
@Override
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { return null;
}
@Override
public List<CustomAdHandler> retrieveCustomAdPlaybackHandlers(MediaPlayerItem item) { return null;
}
};
```

**제로 길이 광고 나누기**

TVSDK 2.5는 광고 서버가 광고를 반환하지 않을 때 길이 제로 광고 나누기를 장소 소유자로 삽입합니다.

onAdBreakStarted 이벤트를 사용하여 광고 브레이크에서 0이 되는 광고 수를 감지하여 길이 제로 광고 브레이크를 결정할 수 있으며 애플리케이션에서 이에 따라 이러한 광고 나누기를 처리해야 합니다.

**메타데이터 변경 사항**

Metadata 클래스는 이전 MetadataNode 클래스를 대체할 수 있는 기능을 제공합니다.

* Metadata 클래스는 문자열, 바이트 배열 및 기타 메타데이터 개체를 저장할 수 있습니다.

```java
TVSDK v1.4
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new MetadataNode();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingParameters(advertisingParams);

return adSettings;
}
//TVSDK v2.5
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new Metadata();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingInfo(advertisingParams);

return adSettings;
}
```

* 열거형이 `MetadataKeys` 바뀝니다 `DefaultMetadataKeys`. 새 버전에 있는 모든 키가 `DefaultMetadataKeys` 있는 것은 아닙니다.

```java
//TVSDK v1.4
if (this.mediaPlayer != null && this.mediaPlayer.getCurrentItem() != null) { MetadataNode resourceMetadata =
(MetadataNode) this.mediaPlayer.getCurrentItem().getResource().getMetadata();
VideoAnalyticsMetadata vaMetadata = (VideoAnalyticsMetadata)
resourceMetadata.getNode(DefaultMetadataKeys.
VIDEO_ANALYTICS_METADATA_KEY.getValue());
}

//TVSDK v2.5
if (resourceMetadata.containsKey(VideoAnalyticsMetadata.
VIDEO_ANALYTICS_METADATA_KEY)) {
JSONObject vaMetadataObj =
new JSONObject(resourceMetadata.
getValue(VideoAnalyticsMetadata. VIDEO_ANALYTICS_METADATA_KEY));
vaMetadata = parseVideoAnalyticsMetadata(vaMetadataObj);
}

} catch (JSONException e) { e.printStackTrace();
}
```

* 광고 메타데이터는 이제 메타데이터의 하위 클래스인 `AdvertisingMetadata` 클래스로 표현되며, 이제 `MediaPlayerItemConfig` 대신 에 저장됩니다 `MediaResource`.

```java
//TVSDK v1.4
MetadataNode mediaMetadata = new MetadataNode();

if (stream.live) { mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(),
getAdSettingsForLive());
} else {
mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(), getAdSettingsForVod());
}
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

if (stream.live) {
AuditudeSettings adSettings = getAdSettingsForLive(); adSettings.setLivePreroll(true); mediaItemConfig.setAdvertisingMetadata(adSettings);
} else {
// Set the advertising parameters for VOD. mediaItemConfig.setAdvertisingMetadata(getAuditudeSettingsForVod());
}

// Create advertising metadata node Metadata mediaMetadata = new Metadata();

// Asset Url
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, mediaMetadata);
try {
mediaPlayer.replaceCurrentResource(playerResource, mItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
//handle exception.
}
```

이전에 `MediaResource` 클래스의 멤버였던 네트워크 구성 메타데이터는 이제 `NetworkConfiguration` 클래스로 표현되며, 이제는 `MediaPlayerItemConfig` 대신 에 저장됩니다 `MediaResource`.

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**TimedMetadata 구문 분석 변경 사항**

ID3 태그 구문 분석을 위한 데이터 유형과 관련하여 2.5에서 구문 분석이 `TimedMetadata` 변경되었습니다.

```java
//TVSDK v1.4
public void onTimedMetadata(TimedMetadata timedMetadata) { TimedMetadata.Type type = timedMetadata.getType();
if (type.equals(TimedMetadata.Type.ID3)){ PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata(); Set<String> keys = metadata.keySet();
for (String key : keys) {
String value = metadata.getValue(key); PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"Key = " + key + " Value = " + value);
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { parseSCTE35Tag(timedMetadata);
}
}
}

//TVSDK v2.5
public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { PMPDemoApp.logger.i(LOG_TAG + " inside"," ontimedmetadata"); TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata();

TimedMetadata.Type type = timedMetadata.getType(); if (type.equals(TimedMetadata.Type.ID3)) {
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata();
if (metadata != null) { PMPDemoApp.logger.i(LOG_TAG +
"::expandID3Metadata", "isEmpty " + metadata.isEmpty());
Set<String> keys = metadata.keySet(); PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"No of keys=" + keys.size());
String s;
for (String key : keys) {
byte[] value = metadata.getByteArray(key); s = new String(value);
if (key.equalsIgnoreCase("APIC"))
s = "SUPPRESSING BINARY DATA FOR ATTACHED PICTURE.";
PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"Key=" + key + ", Length=" + value.length + ", Value=" + s.trim());
}
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { PMPDemoApp.logger.i(LOG_TAG +
" inside ontimedmetadata"," ext"); parseSCTE35Tag(timedMetadata);
}
}
}
```

**기타 변경 사항**

버전 2.5에서는 다음과 같은 추가 변경 사항을 사용할 수 있습니다.

* 이 `notifyClick()` 방법은 에서 `MediaPlayerView` 로 `MediaPlayer`이동되었습니다.

* `AdPolicySelector` 는 클래스가 아닌 인터페이스입니다. 모든 메서드를 구현합니다.
* `AdPolicyInfo` 에는 목록이 `AdBreakTimelineItem`포함되어 있지 않습니다 `AdBreakPlacement`.

* 추상 클래스의 API 이름이 `ContentResolver` 변경되었습니다.
* `PlacementOpportunityDetector` 더 이상 사용할 수 없습니다. 대신 `OpportunityGenerator` 추상 클래스를 확장합니다. 참조 구현에서는 이러한 예를 제공합니다.

* 생성자의 매개 변수는 `AdBreakPlacement` 동일하지만 순서가 다릅니다. 샘플 구현은 제품과 함께 번들로 제공되는 참조 플레이어 구현을 참조하십시오.

## DRM의 변경 사항 {#changes-in-drm}

이 버전에서 대부분의 변경 사항은 DRM 레이어에 있습니다. 다음 표는 버전 1.4와 2.5 간의 추가 변경 사항을 보여 줍니다.

| DRMManager 메서드 | 1.4의 성공 콜백 | 1.4의 오류 콜백 | 2.5의 리스너 |
|--- |--- |--- |--- |
| acquireLicense | DRMLicenseAcquisedCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| acquirePreviewLicense | DRMLicenseAcquisedCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| authenticate | DRMAuthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | 북미 | DRMOperationErrorCallback | DRMErrorListener |
| 초기화 | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leaveLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| resetDRM | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| returnLicense | DRMLicenseReturnCompleteCallback | DRMOperationErrorCallback | DRMReturnLicenseListener |
| setAuthenticationToken | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| storeLicenseBytes | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |

```java
//TVSDK 1.4
private final MediaPlayer.DRMEventListener _drmEventListener = new MediaPlayer.DRMEventListener() {

@Override
public void onDRMMetadata(final DRMMetadataInfo drmMetadataInfo) { PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata available
// event and the play event, so launch the metadata interface
// and give it the loaded metadata bytes, but only once
_drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo == null ||
!DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG + "#onDRMMetadata", "DRM auth is not needed."); return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold
// between the current player time and the DRM metadata start
// time. For the time being, we resolve it as soon as we receive
// the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG + "#onDRMMetadata", "DRMManager is null."); return;
}
SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity()); String authUser =
sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG + "#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(long majorCode,
long minorCode, Exception e) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + majorCode + " 0x" + Long.toHexString(minorCode));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};

//TVSDK 2.5
private final DRMMetadataInfoEventListener drmMetadataInfoEventListener = new DRMMetadataInfoEventListener() {
@Override
public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { final DRMMetadataInfo drmMetadataInfo =
drmMetadataInfoEvent.getDRMMetadataInfo();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata
// available event and the play event, so launch the
// metadata interface and give it the loaded metadata
// bytes, but only once
drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo ==
null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG +
"#onDRMMetadata",
"DRM auth is not needed.");
return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold between
// the current player time and the DRM metadata start time. For the
// time being, we resolve it as soon as we receive the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG +
"#onDRMMetadata", "DRMManager is null.");
return;
}

SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity());
String authUser = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(int major,
int minor,
String erroString, String serverErrorURL) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + major +
" 0x" +
Long.toHexString(minor));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};
```

이제 미디어 레이어가 만들어진 후 1.4에서 사용할 수 있었던 정적 `DRMManager` 인스턴스를 `onDRMMetadataInfo` 이벤트 리스너가 트리거된 후에 사용할 수 있습니다.

## 적응형 비트 전송률(ABR) 관련 변경 사항 {#adaptive-bitrate-abr-related-changes}

**상수 변경 사항**

많은 상수가 문자를 에서 `String` 로 변경했습니다 `int`. 예: `MediaResourceType`및 `ABRControlParameters`를 `MediaPlayerStatusChangeEvent`참조하십시오.

```java
//TVSDK v1.4
ABRControlParameters
private void setAbrControlParams() { SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity());
if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED,
PMPDemoApp.DEFAULT_ABR_ENABLED)) {
int initialBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE, 0);
int minBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE, 0);
int maxBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE, PMPDemoApp.DEFAULT_MAX_BIT_RATE);
int mbrPolicyAsInt =
getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, 0); ABRControlParameters.ABRPolicy abrPolicy = policyFromInt(mbrPolicyAsInt); abrPolicy = abrPolicy != null ?
abrPolicy : ABRControlParameters.ABRPolicy.ABR_MODERATE;
_mediaPlayer.setABRControlParameters(new ABRControlParameters(initialBitRate,
minBitRate, maxBitRate, abrPolicy));
}
}

//TVSDK v2.5
ABRControlParameters
private void setAbrControlParams() { ABRControlParametersBuilder abrBuilder =
new ABRControlParametersBuilder();

if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED, PMPDemoApp.DEFAULT_ABR_ENABLED)) {

abrBuilder.setInitialBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE,
ABRControlParameters.DEFAULT_ABR_INITIAL_BITRATE)); abrBuilder.setMinBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxPlayoutRate(getDoublePreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_PLAYOUT_RATE,
ABRControlParameters.DEFAULT_MAX_PLAYOUT_RATE)); abrBuilder.setMinTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxTrickPlayBandwidthUsage(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BANDWIDTH,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE));

switch (getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, -1)) {
case 0: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_CONSERVATIVE); break;
case 1: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_MODERATE); break;
case 2: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_AGGRESSIVE); break;
default: abrBuilder.setPolicy(ABRControlParameters.DEFAULT_ABR_POLICY);
}
}
_mediaPlayer.setABRControlParameters(abrBuilder.toABRControlParameters());
}
```

**ABRControlParameters 생성자 변경 사항**

일부 매개 변수가 추가되고 이름이 변경되었으며 일부 매개 변수가 이동되었습니다. v1.4의 생성자 서명과 2.5의 새로운 서명은 다음과 같습니다.

```java
//TVSDK v1.4
public ABRControlParameters(ABRPolicy abrPolicy,
int nInitialBitRate, int nMinBitRate,
int nMaxBitRate)

//TVSDK v2.5
public ABRControlParameters(int nInitialBitRate,
int nMinBitRate, int nMaxBitRate,
ABRPolicy abrPolicy,
int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate,
int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate)
```

## 오류 이벤트 및 처리 {#error-events-and-handling}

**오류 처리 변경 사항**

그 `MediaError` 반은 이미 `Notification` 학급으로 대체되었다. 클래스와 클래스 간의 유일한 차이점은 `MediaError` 후자에 description 속성이 `Notification` 없다는 것입니다. TVSDK 2.5에는 101xxx, 102xxx,104xxx,106xxx,107xxx,109xxx 값이 있는 TVSDK 1.4 오류 코드가 없습니다.TVSDK 2.5의 재생 코드는 기본 [오류 - 비디오 재생 값을](assets/psdk_android_2.5.pdf)참조하십시오.

다음은 TVSDK 1.4 및 2.5의 오류 처리 예입니다.

```java
//TVSDK v1.4
@Override
public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");

switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR: PMPDemoApp.logger.e(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: " + notification + "."); getActivity().finish();
break;
default:
// do nothing
}
}

//TVSDK v2.5
private final StatusChangeEventListener statusChangeEventListener = new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent mediaPlayerStatusChangeEvent)
{
MediaPlayerStatus state = mediaPlayerStatusChangeEvent.getStatus(); PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");
switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR:
PMPDemoApp.logger.e(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: ");
printErrorMetadata(mediaPlayerStatusChangeEvent.getMetadata()); showToast("MediaPlayer status ERROR: Look at the logs for details"); getActivity().finish();
break;
default:
// do nothing
}
}
};
```

복구 가능한 모든 오류는 경고로 처리되고 TVSDK 2.5 `NotificationEventListener` 에서 을 사용하여 처리됩니다.경고는 TVSDK 2.5에서와 같이 TVSDK 1.4 `onOperationFailed` 의 QOS 핸들러에서 수신기와 함께 알림으로 표시됩니다. 여기서 알림은 별도의 이벤트입니다. 1.4 및 2.5에서 처리된 경고는 다음과 같습니다.

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener()
{
@Override
public void onBufferStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
}
@Override
public void onBufferComplete() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
}
@Override
public void onSeekStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
}
@Override
public void onSeekComplete(long adjustedTime) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
}
@Override
public void onLoadInfo(LoadInfo loadInfo) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize() + " bytes, media duration: " + loadInfo.getMediaDuration() + "ms, download duration: " + loadInfo.getDownloadDuration() + "ms");
}
@Override
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - ").append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append

//TVSDK v2.5
private final NotificationEventListener notificationEventListener = new NotificationEventListener() {
/**
* An example of dumping the information within a Notification. Here, we don't handle the event in
* any way except to print a log message.
* @param event The NotificationEvent
*/
@Override
public void onNotification(NotificationEvent event) { Notification notification = event.getNotification(); Notification.Type type = notification.getType(); StringBuilder sb = new StringBuilder(); sb.append("[").append(type).append("]");
sb.append(" Player operation failed (").append(notification.getCode()).append(")"); Metadata metadata = notification.getMetadata();
if (metadata != null)
{
for (String key : metadata.keySet())
{
sb.append(", ").append(key).append(" = ").append(metadata.getValue(key));
}
}
Notification inner = notification.getInnerNotification(); if (inner != null) {
sb.append(" :: Inner Notification [").append(inner.getType()).append("](").append(inner.getCode()).append(")");
Metadata innerMetadata = inner.getMetadata(); if (innerMetadata != null) {
for (String iKey : innerMetadata.keySet()) { sb.append(", ").append(iKey).append(" =
").append(innerMetadata.getValue(iKey));
}
}
}
switch(type)
{
case ERROR:
PMPDemoApp.logger.e(LOG_TAG, sb.toString()); break;
case WARNING:
PMPDemoApp.logger.w(LOG_TAG, sb.toString()); break;
default:
PMPDemoApp.logger.i(LOG_TAG, sb.toString()); break;
}
showToast(sb.toString()); PMPDemoApp.logger.d(LOG_TAG, sb.toString());
}
};
```

**새로운 예외**

TVSDK v1.4는 null, 오류 반환 및 다양한 예외( `MediaPlayerException`, `IllegalStateException`및 `IllegalArgumentException`)의 조합을 사용했지만 모든 오류에 대해 TVSDK v2.5 `generatesMediaPlayerException` 를 사용했습니다.

>[!NOTE]
>
>MediaPlayerException에 대한 자세한 내용은 를 참조하십시오 `getErrorCode()`.

변경 사항의 예는 다음과 같습니다.

```java
//TVSDK v1.4
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (IllegalArgumentException e) { PrimetimeReference.logger.w(LOG_TAG +
"#setBufferControlParams",
"Unable to apply buffering params: " + e.getMessage() + ".");
}
}

//TVSDK v2.5
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (MediaPlayerException e) { PrimetimeReference.logger.w(LOG_TAG + "#setBufferControlParams", "Unable to apply buffering params: " + e.getMessage() + ".");
}
}
```

## QOS 매개 변수 변경 사항 {#changes-to-qos-parameters}

QOSProvider 개체 속성에 사소한 변경 사항이 있습니다.

* TVSDK 2.5에서는 `TimeToFirstFrame` 이 기능을 사용할 수 없습니다.
* TVSDK 2.5 QOSProvider는 스트리밍 세션 동안 인식된 대역폭을 확인하는 새로운 속성을 제공합니다.

```java
//TVSDK v1.4
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitrate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); setQosItem("Time to first frame", (int) playbackInformation.getTimeToFirstFrame()); setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); setQosItem("Last seek time", (int) playbackInformation.getLastSeekTime());
}

//TVSDK v2.5
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitRate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart());
setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare());
setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());
```

* TVSDK 2.5에는 더 이상 존재하지 `QOSEventListener::onOperationFailed()` 않습니다.이제 이 이벤트 리스너에 나타나는 경고가 `NotificationEventListener::onNotification()` 이벤트 리스너에 표시됩니다.

* mediaPlayer 인스턴스와 바인딩되는 `QOSProvider event listeners onBufferStart()`개별 이벤트 `onBufferComplete()`리스너와 `onSeekStart()``onSeekComplete()``onLoadInfo()` 같은 세 가지 이벤트 리스너가 있습니다.

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener() {

@Override
public void onBufferStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
@Override
public void onBufferComplete() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
hideBufferingSpinner();
}
@Override
public void onSeekStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
@Override
public void onSeekComplete(long adjustedTime) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " +
adjustedTime + ".");
_controlBar.setPosition(adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayer.PlayerState.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
@Override
public void onLoadInfo(LoadInfo loadInfo) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " +
loadInfo.getUrl() + ", size: " + loadInfo.getSize() +
" bytes, media duration: " +
loadInfo.getMediaDuration() + "ms, download duration: " +
loadInfo.getDownloadDuration() + "ms");
 
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - "). append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append(key).append(": ").
append(metadata.getValue(key));
}
}
innerNotification = innerNotification.getInnerNotification();
}
String errMsg = sb.toString(); PMPDemoApp.logger.w(LOG_TAG +
"::MediaPlayer.QOSEventListener#onOperationFailed()", errMsg);
showToast(errMsg);
}
};

//TVSDK v2.5
mediaPlayer.addEventListener(MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE,
loadInfoEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_BEGIN,
bufferingBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_END,
bufferingEndEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_BEGIN,
seekBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_END,
seekEndEventListener);
// Buffering events.
BufferingBeginEventListener bufferingBeginEventListener = new BufferingBeginEventListener() {
@Override
public void onBufferingBegin(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
};

BufferingEndEventListener bufferingEndEventListener = new BufferingEndEventListener() {
@Override
public void onBufferingEnd(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()",
"Buffering complete."); hideBufferingSpinner();
}
};

BufferPreparedEventListener bufferPreparedEventListener = new BufferPreparedEventListener() {
@Override
public void onBufferPrepared() {
}
};
// seek events.
SeekBeginEventListener seekBeginEventListener = new SeekBeginEventListener() {

@Override
public void onSeekBegin(SeekEvent seekEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
};
SeekEndEventListener seekEndEventListener = new SeekEndEventListener() {
@Override
public void onSeekEnd(SeekEvent seekEvent) {
double adjustedTime = seekEvent.getActualPosition();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
_controlBar.setPosition((long) adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayerStatus.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
};
/**
* LoadInformationEventListener that intercepts PSDK load info events
*/
private final LoadInformationEventListener loadInfoEventListener = new LoadInformationEventListener() {

@Override
public void onLoadInformation(LoadInformationEvent event) { LoadInformation loadInfo = event.getLoadInfomation(); PMPDemoApp.logger.i(
LOG_TAG + "::LoadInformationEventListener#onLoadInfomation()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize()
+ " bytes, download duration: "
+ loadInfo.getDownloadDuration() + "ms");
}
};
```

## 유용한 리소스 {#helpful-resources}

* Adobe Primetime 학습 및 지원 [페이지에서 전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.