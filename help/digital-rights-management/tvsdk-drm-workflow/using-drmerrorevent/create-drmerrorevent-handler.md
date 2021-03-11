---
title: DRMErrorEvent 핸들러 만들기
description: DRMErrorEvent 핸들러 만들기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# DRMErrorEvent 핸들러 만들기{#create-a-drmerrorevent-handler}

보호된 콘텐츠를 재생하는 동안 오류가 발생할 때 Primetime에서 전달된 오류 이벤트를 처리할 이벤트 핸들러를 만듭니다.

일반적으로 응용 프로그램에 오류가 발생하면 많은 수의 정리 작업을 수행합니다. 그런 다음 사용자에게 오류를 알리고 문제를 해결하기 위한 옵션을 제공합니다.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

