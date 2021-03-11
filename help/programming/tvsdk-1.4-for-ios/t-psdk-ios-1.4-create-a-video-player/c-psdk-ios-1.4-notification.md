---
description: 플레이어는 플레이어의 상태를 나타내는 다양한 이벤트를 수신할 수 있습니다.
title: 알림 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# 알림 설정{#set-up-notifications}

플레이어는 플레이어의 상태를 나타내는 다양한 이벤트를 수신할 수 있습니다.

`PTMediaPlayer`이(가) 클라이언트 플레이어의 속성이라고 가정할 때 다음 예제의 `self.player`은 `PTMediaPlayer` 인스턴스를 나타냅니다. 다음 예제에서는 PTMediaPlayer 설정 지침에 표시되는 `addObservers` 메서드를 구현하고 대부분의 알림을 포함합니다.

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerStatusChange:)  
      name:PTMediaPlayerStatusNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
      name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
      name:PTMediaPlayerTimeChangeNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemPlayStarted:)  
      name:PTMediaPlayerPlayStartedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemPlayCompleted:)  
      name:PTMediaPlayerPlayCompletedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemTimelineChanged:)  
      name:PTMediaPlayerTimelineChangedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
      name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
      name:PTMediaPlayerAdBreakStartedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
      name:PTMediaPlayerAdBreakCompletedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdPlayStarted:)  
      name:PTMediaPlayerAdStartedNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdPlayProgress:)  
      name:PTMediaPlayerAdProgressNotification object:self.player]; 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdPlayCompleted:)  
      name:PTMediaPlayerAdCompletedNotification object:self.player]; 
```

## iOS 알림 {#section_65D9B2DBF5574313BD3218AB02242BBB}

`ThePTMediaPlayerNotifications` 클래스는 TVSDK가 플레이어에 전달하는 알림을 나열합니다.

<table frame="all" colsep="1" rowsep="1" id="table_ios_notifications"> 
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>알림</b> </td> 
   <td colname="2"> <b>의미</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdBreakCompletedNotification  </span> </td> 
   <td colname="2"> 광고 중단이 종료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdBreakStartedNotification  </span> </td> 
   <td colname="2"> 광고 중단이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdClickNotification  </span> </td> 
   <td colname="2"> 사용자가 배너 광고를 클릭했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdCompletedNotification  </span> </td> 
   <td colname="2"> 개별 광고가 종료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdProgressNotification  </span> </td> 
   <td colname="2"> 광고물광고가 재생되는 동안 지속적으로 전달됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerAdStartedNotification  </span> </td> 
   <td colname="2"> 개별 광고가 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTBackgroundManifestErrorNotification  </span> </td> 
   <td colname="2"> 백그라운드 매니페스트를 다운로드하지 못했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerBufferingCompletedNotification  </span> </td> 
   <td colname="2"> 버퍼링이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerBufferingStartedNotification  </span> </td> 
   <td colname="2"> 미디어 플레이어가 버퍼링 상태로 전환됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTAudioTrackChangeCompleted  </span> </td> 
   <td colname="2"> 현재 재생 중인 미디어의 오디오 트랙에 대한 변경이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTAudioTrackChangeStarted  </span> </td> 
   <td colname="2"> 현재 재생 중인 미디어의 오디오 트랙에 대한 변경 사항이 시작됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerItemChangedNotification  </span> </td> 
   <td colname="2"> <span class="codeph"> PTMediaPlayer </span>의 다른 <span class="codeph"> PTMediaPlayerItem </span>이(가) 설정되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerItemDRMMetadataChanged  </span> </td> 
   <td colname="2"> DRM 메타데이터가 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerMediaSelectionOptionsAvailableNotification  </span> </td> 
   <td colname="2"> 새 자막과 대체 오디오 트랙이 있습니다( <span class="codeph"> PTMediaSelectionOption </span>). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerNewNotificationEntryAddedNotification  </span> </td> 
   <td colname="2"> 알림 이벤트가 알림 기록에 추가될 때, 즉 현재 <span class="codeph"> PTMediaPlayerItem </span>의 <span class="codeph"> PTNotificationHistoryItem </span>에 새 <span class="codeph"> PTNotificationHistoryItem </span>이(가) 추가되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerPlayCompletedNotification  </span> </td> 
   <td colname="2"> 미디어 재생이 종료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerSeekCompletedNotification  </span> </td> 
   <td colname="2"> 검색이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerSeekErrorNotification  </span> </td> 
   <td colname="2"> 현재 검색 작업에 실패했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerSeekStartedNotification  </span> </td> 
   <td colname="2"> 검색 시작. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerPlayStartedNotification  </span> </td> 
   <td colname="2"> 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerStatusNotification  </span> </td> 
   <td colname="2"> 플레이어 상태가 변경되었습니다. 가능한 상태 값은 다음과 같습니다. 
    <ul id="ul_DDBE8CAD5D5A46D2AAA6B98F0754A881"> 
     <li id="li_48F9AD580BCB4BB8A5C2DFED0DF9970F"> <p> <span class="codeph"> PTMediaPlayerStatusCreated  </span> </p> </li> 
     <li id="li_EDFB0765CF14422A95C9119DA3394163"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing  </span> </p> </li> 
     <li id="li_06E1576D50C646C19E88F0F14912F2C0"> <p> <span class="codeph"> PTMediaPlayerStatusInitialized  </span> </p> </li> 
     <li id="li_E8B7157B5B234DFFABC2E5BEC241AB84"> <p> <span class="codeph"> PTMediaPlayerStatusReady  </span> </p> </li> 
     <li id="li_FF2E66B390154EAA8791B4D874CC62E1"> <p> <span class="codeph"> PTMediaPlayerStatusPlaying  </span> </p> </li> 
     <li id="li_6F3306832B7642E4BEE84068383AFAF3"> <p> <span class="codeph"> PTMediaPlayerStatusPaused  </span> </p> </li> 
     <li id="li_AE579AB888954F89A7F1115CAC0655E6"> <p> <span class="codeph"> PTMediaPlayerStatusStopped  </span> </p> </li> 
     <li id="li_A4CEB39374E84B4AA4F7202E67B9BE43"> <p> <span class="codeph"> PTMediaPlayerStatusCompleted  </span> </p> </li> 
     <li id="li_C50EB9C459264641A9FF70EF901D7474"> <p> <span class="codeph"> PTMediaPlayerStatusError  </span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerTimeChangeNotification  </span> </td> 
   <td colname="2"> 재생 현재 시간이 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTMediaPlayerTimelineChangedNotification  </span> </td> 
   <td colname="2"> 현재 플레이어 타임라인이 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" colsep="1" rowsep="1"> <span class="codeph"> PTTimedMetadataChangedNotification  </span> </td> 
   <td colname="2"> TVSDK에서 가입된 태그가 처음 발생했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> PTTimedMetadataChangedInBackgroundNotification  </span> </td> 
   <td colname="2"> <p>구독된 태그가 배경 매니페스트에서 식별되고 이 태그에서 새 <span class="codeph"> PTTimedMetadata </span> 인스턴스가 준비됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 알림용 샘플 핸들러 {#section_D729C2403A234DD09596829D26882ADC}

다음 코드 조각은 알림을 사용할 수 있는 몇 가지 방법을 보여 줍니다.

`PTMediaPlayerAdBreakKey`을(를) 사용하여 `PTAdBreak` 인스턴스를 가져옵니다.

```
 - (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification { 
   // Fetch the PTAdBreak instance using PTMediaPlayerAdBreakKey 
   PTAdBreak *adBreak = [notification.userInfo objectForKey:PTMediaPlayerAdBreakKey]; 
   ... 
   ... 
} 
```

`subtitlesOptions` 및 `audioOptions` 설정:

```
 - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification \*) notification { 
   //SubtitlesOptions and audioOptions are set and accessible now. 
   NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions;  
   NSArray* audioOp tions = self.player.currentItem.audioOptions; 
   ... 
   ... 
} 
```

`PTMediaPlayerAdKey`을(를) 사용하여 `PTAd` 인스턴스를 가져옵니다.

```
 - (void) onMediaPlayerAdPlayStarted:(NSNotification \*)  notification { 
   // Fetch the PTAdinstance using PTMediaPlayerAdKey 
   PTAd *ad = [notification.userInfo objectForKey:PTMediaPlayerAdKey]; 
   ... 
   ... 
} 
```

