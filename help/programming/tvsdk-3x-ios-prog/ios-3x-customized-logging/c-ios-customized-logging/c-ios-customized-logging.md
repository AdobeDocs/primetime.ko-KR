---
description: 자체 로깅 시스템을 구현할 수 있습니다.
seo-description: 자체 로깅 시스템을 구현할 수 있습니다.
seo-title: 맞춤형 로깅 이해
title: 맞춤형 로깅 이해
uuid: f056d7d7-ec3a-4cf1-997f-72a89bbc9447
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 사용자 지정된 로깅 {#customized-logging}

자체 로깅 시스템을 구현할 수 있습니다.

미리 정의된 알림을 사용하여 로깅하는 것 외에도 TVSDK에서 생성된 로그 메시지와 메시지를 사용하는 로깅 시스템을 구현할 수 있습니다. 사전 정의된 알림에 대한 자세한 내용은 [알림 시스템](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System)을 참조하십시오. 이러한 로그를 사용하여 플레이어 응용 프로그램의 문제를 해결하고 재생 및 광고 작업 과정을 더 잘 이해할 수 있습니다.

사용자 지정된 로깅은 여러 로거에 메시지를 로깅하는 메커니즘을 제공하는 `PSDKPTLogFactory`의 공유 단일 인스턴스를 사용합니다. 하나 이상의 로거를 정의하고 `PTLogFactory`에 추가(등록)합니다. 콘솔 로거, 웹 로거 또는 콘솔 기록 로거 등 사용자 정의 구현을 통해 여러 로거를 정의할 수 있습니다.

TVSDK는 많은 해당 활동에 대한 로그 메시지를 생성하며, 이 경우 `PTLogFactory`은 등록된 모든 로거 대상으로 전달됩니다. 또한 애플리케이션에서 사용자 정의 로그 메시지를 생성하여 등록된 모든 로거에게 전달할 수 있습니다. 각 로거는 메시지를 필터링하고 적절한 작업을 수행할 수 있습니다.

`PTLogFactory`에 대한 두 가지 구현이 있습니다.

* 로그 의견 수렴
* `PTLogFactory`에 로그를 추가하려면

## 로그 수신{#listen-to-logs}

로그 의견 수렴을 위해 등록하려면
1. 프로토콜 `PTLogger`을 따르는 사용자 지정 클래스를 구현합니다.

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

1. 로깅 항목을 수신할 인스턴스를 등록하려면 `PTLogger` 인스턴스를 `PTLoggerFactory`에 추가합니다.

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

## 새 로그 메시지 {#add-new-log-messages} 추가

로그들을 위해 등록하려면

새 `PTLogEntry`을(를) 만들고 `thePTLogFactory`에 추가합니다.

`PTLogEntry`을 수동으로 인스턴스화하고 `PTLogFactory` 공유 인스턴스에 추가하거나 매크로 중 하나를 사용하여 동일한 작업을 수행할 수 있습니다.

다음은 `PTLogDebug` 매크로를 사용한 로깅의 예입니다.

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
