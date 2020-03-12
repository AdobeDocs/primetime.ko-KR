---
description: 자체 로깅 시스템을 구현할 수 있습니다.
seo-description: 자체 로깅 시스템을 구현할 수 있습니다.
seo-title: 사용자 정의 로깅
title: 사용자 정의 로깅
uuid: c5bdf266-4266-4896-b6e0-47710ce64e67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 정의 로깅 {#customized-logging}

자체 로깅 시스템을 구현할 수 있습니다.

미리 정의된 알림을 사용하여 로깅하는 것 외에도 TVSDK에서 생성된 로그 메시지와 메시지를 사용하는 로깅 시스템을 구현할 수 있습니다. 사전 정의된 알림에 대한 자세한 내용은 알림 [시스템을 참조하십시오](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). 이러한 로그를 사용하여 플레이어 응용 프로그램의 문제를 해결하고 재생 및 광고 작업 과정에 대한 이해를 높일 수 있습니다.

사용자 정의 로깅은 여러 로거에 메시지를 로깅하는 메커니즘을 제공하는 `PSDKPTLogFactory`의 공유 singleton 인스턴스를 사용합니다. 하나 이상의 로거를 정의 및 추가하여(등록) `PTLogFactory`합니다. 콘솔 로거, 웹 로거 또는 콘솔 기록 로거와 같은 사용자 정의 구현을 통해 여러 로거를 정의할 수 있습니다.

TVSDK는 많은 활동에 대한 로그 메시지를 생성하며, 이렇게 하면 등록된 모든 로거에게 `PTLogFactory` 전달됩니다. 또한 애플리케이션에서 사용자 정의 로그 메시지를 생성하여 등록된 모든 로거에게 전달할 수 있습니다. 각 로거는 메시지를 필터링하고 적절한 작업을 수행할 수 있습니다.

다음 두 가지 구현 방법이 `PTLogFactory`있습니다.

* 로그 의견 수렴
* 에 로그를 추가하는 `PTLogFactory`경우

## 로그 수신 {#listen-to-logs}

로그 의견 수렴을 위해 등록하려면
1. 프로토콜을 따르는 사용자 지정 클래스를 `PTLogger`구현합니다.

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

1. 로깅 항목을 수신할 인스턴스를 등록하려면 다음 항목에 `PTLogger` 의 인스턴스를 추가합니다 `PTLoggerFactory`.

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

다음은 `PTLogEntry` 유형을 사용하여 로그를 필터링하는 예입니다.

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

로그를 수신하기 위해 등록하려면
1. 새로 `PTLogEntry` 만들고 다음에 추가합니다 `thePTLogFactory`.

   수동으로 `PTLogEntry` `PTLogFactory` 인스턴스화하고 공유 인스턴스에 추가하거나 매크로 중 하나를 사용하여 동일한 작업을 수행할 수 있습니다.

   다음은 `PTLogDebug` 매크로를 사용한 로깅의 예입니다.

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
