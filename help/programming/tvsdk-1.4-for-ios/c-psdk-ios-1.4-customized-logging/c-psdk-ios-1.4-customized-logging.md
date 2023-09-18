---
description: 고유한 로깅 시스템을 구현할 수 있습니다.
title: 사용자 지정된 로깅
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 사용자 지정된 로깅 {#customized-logging}

고유한 로깅 시스템을 구현할 수 있습니다.

사전 정의된 알림을 사용하여 로깅하는 것 외에도, TVSDK에서 생성한 로그 메시지와 메시지를 사용하는 로깅 시스템을 구현할 수 있습니다. 사전 정의된 알림에 대한 자세한 내용은 [알림 시스템](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). 이러한 로그를 사용하여 플레이어 애플리케이션 문제를 해결하고 재생 및 광고 작업 과정을 더 잘 이해할 수 있습니다.

사용자 지정된 로깅은 의 공유 단일 인스턴스를 사용합니다. `PSDKPTLogFactory`: 여러 로거에 메시지를 기록하는 메커니즘을 제공합니다. 하나 이상의 로거를 정의하고 (등록) `PTLogFactory`. 이렇게 하면 콘솔 로거, 웹 로거 또는 콘솔 기록 로거와 같은 사용자 지정 구현으로 여러 로거를 정의할 수 있습니다.

TVSDK는 다음과 같은 여러 활동에 대한 로그 메시지를 생성합니다. `PTLogFactory` 등록된 모든 로거에게 전달됩니다. 또한 애플리케이션은 등록된 모든 로거에게 전달되는 사용자 정의 로그 메시지를 생성할 수 있습니다. 각 로거는 메시지를 필터링하고 적절한 조치를 취할 수 있습니다.

에는 두 가지 구현이 있습니다 `PTLogFactory`:

* 로그 감상.
* 에 로그를 추가하는 경우 `PTLogFactory`.

## 로그 수신 {#listen-to-logs}

로그 수신을 등록하려면:
1. 프로토콜을 따르는 사용자 지정 클래스 구현 `PTLogger`:

   ```
   @implementation PTConsoleLogger 
   
   + (PTConsoleLogger *) consoleLogger { 
       return [[[PTConsoleLogger alloc] init] autorelease]; 
   } 
   
   - (void)logEntry:(PTLogEntry *)entry { 
       //Log the message to the console using NSLog  
       NSLog(@"[%@] %@", entry.tag, entry.message); 
   } 
   
   @end
   ```

1. 로깅 항목을 수신할 인스턴스를 등록하려면 의 인스턴스를 `PTLogger` (으)로 `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

다음은 를 사용하여 로그를 필터링하는 예제입니다. `PTLogEntry` 유형:

```
@implementation PTConsoleLogger 
 
+ (PTConsoleLogger *) consoleLogger { 
    return [[[PTConsoleLogger alloc] init] autorelease]; 
} 
 
- (id) init { 
    self = [super init]; 
 
    if (self) { 
        self.logLevel = PTLogEntryTypeInfo; 
    } 
 
    return self; 
} 
 
- (void)logEntry:(PTLogEntry *) entry { 
    //Filtering the entry by log level  
    if (entry.type < _logLevel) { 
        return; 
    } 
 
    //Log the message to the console using NSLog NSLog(@"[%@] %@", entry.tag, entry.message); 
} 
 
@end
```

## 새 로그 메시지 추가 {#add-new-log-messages}

로그를 수신하려면 등록하십시오.
1. 새로 만들기 `PTLogEntry` 및 추가 `thePTLogFactory`:

   다음을 수동으로 인스턴스화할 수 있습니다. `PTLogEntry` 및에 추가합니다. `PTLogFactory` 공유 인스턴스 또는 매크로 중 하나를 사용하여 동일한 작업을 수행합니다.

   다음은 를 사용한 로깅의 예입니다. `PTLogDebug` 매크로:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
