---
description: 재생이 광고 브레이크에 도달하거나, 광고 브레이크를 전달하거나, 광고 브레이크에서 종료되면 TVSDK는 현재 플레이헤드의 위치에 대한 몇 가지 기본 동작을 정의합니다.
title: 광고를 사용하여 재생 사용자 지정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# 광고를 사용하여 재생 사용자 지정{#customize-playback-with-ads}

재생이 광고 브레이크에 도달하거나, 광고 브레이크를 전달하거나, 광고 브레이크에서 종료되면 TVSDK는 현재 플레이헤드의 위치에 대한 몇 가지 기본 동작을 정의합니다.

>[!TIP]
>
>다음을 사용하여 기본 동작을 재정의할 수 있습니다. `PTAdPolicySelector` 클래스.

기본 비헤이비어는 사용자가 일반 재생 중에 광고 브레이크를 전달하는지 또는 비디오에서 찾는지에 따라 달라집니다.

다음 방법으로 광고 재생 동작을 사용자 지정할 수 있습니다.

* 사용자가 비디오 보기를 중단한 위치를 저장하고 이후 세션에서 동일한 위치에서 재생을 재개합니다.
* 사용자에게 광고 브레이크가 표시되면 사용자가 새 위치를 찾으려고 하더라도 몇 분 동안 추가 광고를 표시하지 않습니다.
* 몇 분 후에 컨텐츠가 재생되지 않으면 스트림을 다시 시작하거나 동일한 컨텐츠의 다른 소스로 페일오버합니다.

  페일오버 재생 세션에서 사용자가 광고를 건너뛰고 실패한 이전 위치로 다시 시작할 수 있도록 프리롤 및/또는 미드롤 광고를 비활성화할 수 있습니다. TVSDK는 프리롤 및 미드롤 광고를 건너뛸 수 있도록 하는 메서드를 제공합니다.

## 광고 재생용 API 요소 {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK는 광고가 포함된 콘텐츠의 재생 동작을 사용자 지정하는 데 사용할 수 있는 클래스와 메서드를 제공합니다.
다음 API 요소는 재생을 사용자 지정하는 데 유용합니다.

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API 요소 </th> 
   <th colname="col2" class="entry"> 광고를 지원하는 콘텐츠 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> 광고 브레이크를 시청자가 시청한 것으로 표시해야 하는지 여부와 표시해야 하는 시점을 제어합니다. 다음을 사용하여 감시 정책 설정 및 가져오기 <span class="codeph"> adBreakAsWatched </span> 속성. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> TVSDK 광고 동작의 맞춤화를 허용하는 프로토콜입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 기본 TVSDK 동작을 구현하는 클래스입니다. 응용 프로그램에서 이 클래스를 재정의하여 전체 인터페이스를 구현하지 않고도 기본 동작을 사용자 지정할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>이는 배치된 광고 브레이크를 제외한 재생의 로컬 시간입니다. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> . <p>여기에서, 찾기는 스트림 내의 로컬 시간에 관하여 발생한다. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>타임라인에서 가상 위치가 로컬 위치로 변환됩니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched </span> 속성. 뷰어가 광고를 시청했는지 여부를 나타냅니다. </td> 
  </tr> 
 </tbody> 
</table>

## 사용자 지정 재생 설정 {#section_8209BAACC7814C9399988DC7DE9CF4CA}

광고 동작을 사용자 정의하거나 재정의하려면 먼저 TVSDK에 광고 정책 인스턴스를 등록합니다.

광고 동작을 사용자 지정하려면 다음 중 하나를 수행하십시오.

* 다음 내용에 부합합니다. `PTAdPolicySelector` 필요한 모든 정책 선택 방법을 프로토콜로 지정하고 구현합니다.

  재정의해야 하는 경우 이 옵션을 권장합니다. **모두** 기본 광고 동작입니다.

* 재정의 `PTDefaultAdPolicySelector` 클래스를 만들고 맞춤화가 필요한 비헤이비어에 대해서만 구현을 제공합니다.

  이 옵션은 재정의해야 하는 경우에만 권장됩니다. **일부** 기본 동작.

두 옵션 모두 다음 작업을 완료하십시오.

1. 클라이언트 팩토리를 통해 TVSDK에서 사용할 정책 인스턴스를 등록합니다.

   >[!NOTE]
   >
   >재생 시작 시 등록된 사용자 지정 광고 정책은 `PTMediaPlayer` 인스턴스가 할당 해제되었습니다. 애플리케이션은 새 재생 세션이 생성될 때마다 정책 선택기 인스턴스를 등록해야 합니다.

   예:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 맞춤화 구현.

## 일정 기간 동안 광고 브레이크 건너뛰기 {#section_99809BE4D9BB4DEEBBF596C746CA428A}

기본적으로 TVSDK는 사용자가 광고 브레이크를 검색할 때 광고 브레이크를 강제로 재생합니다. 이전 브레이크 완료에서 경과된 시간이 특정 분 이내인 경우 광고 브레이크를 건너뛰도록 동작을 사용자 지정할 수 있습니다.

>[!IMPORTANT]
>
>광고를 건너뛰려는 내부 찾기가 있는 경우 재생이 약간 일시 중지될 수 있습니다.

사용자 지정된 광고 정책 선택기의 다음 예제는 사용자가 광고 브레이크를 시청한 후 5분(벽면 시계 시간) 안에 광고를 건너뜁니다.

1. 클라이언트 팩토리를 통해 TVSDK에서 사용할 정책 인스턴스를 등록합니다.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 사용자 지정 구현.

**PTS5MinuteSkipBreakPolicySelector.h**

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m**

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## 비디오 위치를 저장하고 나중에 다시 시작 {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

비디오에서 현재 재생 위치를 저장하고 이후 세션에서 동일한 위치에서 재생을 재개할 수 있습니다.

동적으로 삽입된 광고는 사용자 세션마다 다르므로 위치를 저장합니다. **포함** 스플라이싱된 광고는 향후 세션에서 다른 위치를 나타냅니다. TVSDK는 스플라이싱된 광고를 무시하면서 재생 위치를 검색하는 메서드를 제공합니다.

1. 사용자가 비디오를 종료하면 애플리케이션이 비디오의 위치를 검색하여 저장합니다.

   >[!TIP]
   >
   >광고 기간은 포함되지 않습니다.

   광고 패턴, 빈도 제한 등으로 인해 각 세션에서 광고 브레이크가 달라질 수 있습니다. 한 세션에 있는 비디오의 현재 시간은 향후 세션에서 다를 수 있습니다. 비디오에서 Position을 저장할 때, 애플리케이션은 현지 시간 을 검색합니다. 사용  `localTime` 이 위치를 읽는 속성으로, 장치 또는 서버의 데이터베이스에 저장할 수 있습니다.

   예를 들어 사용자가 비디오의 20분에 있고 이 위치에 5분의 광고가 포함된 경우 `currentTime` 은 1200초가 되고, `localTime` 이 위치에서는 900초가 됩니다.

   >[!IMPORTANT]
   >
   >라이브/선형 스트림의 경우 현지 시간과 현재 시간이 동일합니다. 이 경우, `convertToLocalTime` 은(는) 효과가 없습니다. VOD의 경우 광고가 재생되는 동안 현지 시간은 변경되지 않습니다.

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
   
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. 동일한 위치에서 비디오를 재개하려면: 이전 세션에서 저장된 위치에서 비디오 재생을 재개하려면 를 사용합니다. `seekToLocalTime`

   >[!TIP]
   >
   >이 메서드는 현지 시간 값으로만 호출됩니다. 현재 시간 결과를 사용하여 메서드가 호출되면 잘못된 동작이 발생합니다.

   현재 시간을 찾으려면 다음을 사용합니다 `seekToTime`.

1. 애플리케이션이 `PTMediaPlayerStatusReady` 상태 변경 이벤트에서 저장된 현지 시간으로 이동하십시오.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 광고 정책 인터페이스에 지정된 대로 광고 브레이크를 제공합니다.
1. 기본 광고 정책 선택기를 확장하여 사용자 지정 광고 정책 선택기를 구현합니다.
1. 를 구현하여 사용자에게 표시해야 하는 광고 브레이크를 제공합니다 `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >이 방법에는 프리롤 광고 브레이크와 로컬 시간 위치 이전에 미드롤 광고 브레이크가 포함됩니다. 애플리케이션에서는 프리롤 광고 브레이크를 재생하고 지정된 현지 시간으로 다시 시작하거나, 미드롤 광고 브레이크를 재생하고 지정된 현지 시간으로 다시 시작하거나, 광고 브레이크를 재생하지 않도록 결정할 수 있습니다.
