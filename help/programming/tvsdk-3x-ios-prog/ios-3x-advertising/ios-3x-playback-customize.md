---
description: 재생이 광고 중단에 도달하거나 광고 나누기를 전달하거나 광고 중단으로 끝나는 경우 TVSDK는 현재 재생 헤드의 위치에 대한 몇 가지 기본 동작을 정의합니다.
seo-description: 재생이 광고 중단에 도달하거나 광고 나누기를 전달하거나 광고 중단으로 끝나는 경우 TVSDK는 현재 재생 헤드의 위치에 대한 몇 가지 기본 동작을 정의합니다.
seo-title: 광고로 재생 맞춤화
title: 광고로 재생 맞춤화
uuid: b21a2b1b-5376-41cb-a772-a8945fd56f3c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 광고로 재생 맞춤화 {#customize-playback-with-ads}

재생이 광고 중단에 도달하거나 광고 나누기를 전달하거나 광고 중단으로 끝나는 경우 TVSDK는 현재 재생 헤드의 위치에 대한 몇 가지 기본 동작을 정의합니다.

>[!TIP]
>
>클래스를 사용하여 기본 동작을 재정의할 수 `PTAdPolicySelector` 있습니다.

기본 동작은 사용자가 일반 재생 중에 광고 나누기를 전달하는지 또는 비디오에서 검색하는 방법에 따라 달라집니다.

다음과 같은 방법으로 광고 재생 동작을 사용자 정의할 수 있습니다.

* 사용자가 비디오 시청을 중단한 위치를 저장하고 이후 세션에서 동일한 위치에서 재생을 다시 시작합니다.
* 사용자에게 광고 중단이 표시되는 경우 사용자가 새 위치를 원하는 경우에도 몇 분 동안 추가 광고를 표시하지 않습니다.
* 몇 분 후 컨텐츠가 재생되지 않으면 스트림을 다시 시작하거나 동일한 컨텐츠의 다른 소스로 장애 조치(failover)합니다.

   장애 조치(failover) 재생 세션에서 사용자가 광고를 건너뛰고 실패한 이전 위치로 다시 시작할 수 있도록 프리롤 및/또는 미드롤 광고를 비활성화할 수 있습니다. TVSDK는 프리롤 및 미드롤 광고를 건너뛰는 방법을 제공합니다.

## 광고 재생을 위한 API 요소 {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK 파섹
다음 API 요소는 재생을 사용자 지정하는 데 유용합니다.

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>API 요소</b></th> 
   <th colname="col2" class="entry"><b>광고를 지원하는 컨텐츠</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> 뷰어에서 광고 나누기를 시청한 것으로 표시할지를, 그리고 예인 경우 언제 표시할지를 제어합니다. adBreakAsViewed <span class="codeph"> 속성을 사용하여 감시 정책을 </span> 설정하고 가져옵니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> TVSDK 광고 비헤이비어를 사용자 정의할 수 있는 프로토콜입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDedefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 기본 TVSDK 비헤이비어를 구현하는 클래스입니다. 응용 프로그램은 전체 인터페이스를 구현하지 않고 기본 동작을 사용자 지정하기 위해 이 클래스를 재정의할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> 현지 </span>시간. <p>가져온 광고 브레이크는 제외하고 재생의 현지 시간입니다. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> 을 참조하십시오. <p>여기에서 검색은 스트림의 로컬 시간을 기준으로 수행됩니다. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>을 참조하십시오. <p>타임라인의 가상 위치가 로컬 위치로 변환됩니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isViewed </span> 속성입니다. 뷰어가 광고를 보았는지 여부를 나타냅니다. </td> 
  </tr> 
 </tbody> 
</table>

## 사용자 정의 재생 설정 {#section_8209BAACC7814C9399988DC7DE9CF4CA}

광고 행동을 사용자 정의하거나 무시하려면 먼저 광고 정책 인스턴스를 TVSDK에 등록합니다.

광고 동작을 사용자 정의하려면 다음 중 하나를 수행합니다.

* 프로토콜을 `PTAdPolicySelector` 준수하고 필요한 모든 정책 선택 방법을 구현합니다.

   이 옵션은 **모든** 기본 광고 동작을 재정의해야 하는 경우에 권장됩니다.

* 클래스를 `PTDefaultAdPolicySelector` 재정의하고 사용자 지정이 필요한 비헤이비어에 대해서만 구현을 제공합니다.

   이 옵션은 **일부** 기본 동작만 재정의해야 하는 경우에 권장됩니다.

두 옵션 모두에 대해 다음 작업을 완료하십시오.

1. 클라이언트 팩터리를 통해 TVSDK에서 사용할 정책 인스턴스를 등록합니다.

   >[!NOTE]
   >
   >재생 시작 시 등록된 사용자 정의 광고 정책은 `PTMediaPlayer` 인스턴스가 할당 해제될 때 지워집니다. 응용 프로그램은 새 재생 세션이 생성될 때마다 정책 선택기 인스턴스를 등록해야 합니다.

   예:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 사용자 정의 구현

## 일정 기간 동안 광고 중단 건너뛰기 {#section_99809BE4D9BB4DEEBBF596C746CA428A}

기본적으로 TVSDK는 사용자가 광고 브레이크를 검색할 때 광고 중단이 강제로 발생합니다. 이전 중단 완료에서 경과된 시간이 일정 시간 이내인 경우 광고 나누기를 건너뛸 동작을 사용자 정의할 수 있습니다.

>[!IMPORTANT]
>
>광고를 건너뛰려는 내부 검색이 있는 경우 재생에 약간의 일시 중지가 있을 수 있습니다.

사용자 지정된 광고 정책 선택기의 다음 예는 사용자가 광고 나누기를 본 후 다음 5분(월 시간대) 동안 광고를 건너뜁니다.

1. 클라이언트 팩터리를 통해 TVSDK에서 사용할 정책 인스턴스를 등록합니다.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 사용자 정의 구현

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

## 비디오 위치를 저장하고 나중에 다시 시작합니다. {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

비디오의 현재 재생 위치를 저장하고 이후 세션에서 동일한 위치에서 재생을 다시 시작할 수 있습니다.

동적으로 삽입된 광고는 사용자 세션마다 다르므로 **겹친 광고로 위치를** 저장하는 것은 향후 세션에서 다른 위치를 나타냅니다. TVSDK 파섹

1. 사용자가 비디오를 종료하면 애플리케이션에서 해당 위치를 검색하여 비디오에 저장합니다.

   >[!TIP]
   >
   >광고 기간은 포함되지 않습니다.

   광고 브레이크는 광고 패턴, 빈도 매핑 등으로 인해 각 세션에서 달라질 수 있습니다. 한 세션에서 비디오의 현재 시간은 이후 세션에서 다를 수 있습니다. 비디오의 위치를 저장할 때 응용 프로그램은 현지 시간을 검색합니다. 이 `localTime` 속성을 사용하여 장치 또는 서버의 데이터베이스에 저장할 수 있는 이 위치를 읽습니다.

   예를 들어 사용자가 비디오의 20분 지점에 있고 이 위치에 광고 5분이 포함된 경우 1200초가 `currentTime` 되고 이 `localTime` 위치에는 900초가 됩니다.

   >[!IMPORTANT]
   >
   >실시간/선형 스트림의 경우 로컬 시간과 현재 시간이 동일합니다. 이 경우 아무런 `convertToLocalTime` 효과가 없습니다. VOD의 경우, 광고가 재생되는 동안 현지 시간은 변경되지 않습니다.

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

1. 이전 세션에서 저장한 동일한 위치에서 비디오를 다시 시작하려면 을 `seekToLocalTime`사용합니다.

   >[!TIP]
   >
   >이 메서드는 로컬 시간 값에서만 호출됩니다. 메서드가 현재 시간 결과와 함께 호출되면 잘못된 동작이 발생합니다.

   현재 시간을 검색하려면 을 `seekToTime`사용합니다.

1. 응용 프로그램이 `PTMediaPlayerStatusReady` 상태 변경 이벤트를 받으면 저장된 현지 시간으로 이동합니다.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 광고 정책 인터페이스에 지정된 대로 광고 나누기를 제공합니다.
1. 기본 광고 정책 선택기를 확장하여 사용자 지정 광고 정책 선택기를 구현합니다.
1. 구현하여 사용자에게 제공해야 하는 광고 중단점을 제공합니다. `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >이 방법에는 프리롤 광고 중단과 로컬 시간 위치 이전의 미드롤 광고 브레이크가 포함됩니다. 애플리케이션에서 프리롤 광고 브레이크를 재생하고 지정된 현지 시간으로 다시 시작하거나, 미드롤 광고 브레이크를 재생하고, 지정된 현지 시간으로 다시 시작하거나, 광고 브레이크를 재생하지 않습니다.