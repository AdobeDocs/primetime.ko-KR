---
seo-title: DRMErrorEvent 핸들러 만들기
title: DRMErrorEvent 핸들러 만들기
uuid: dde660fc-6899-47d4-97d4-46acda2db262
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# DRMErrorEvent 핸들러 만들기{#create-a-drmerrorevent-handler}

보호된 콘텐츠를 재생하는 동안 오류가 발생하면 Primetime에서 전달된 오류 이벤트를 처리하는 이벤트 핸들러를 만듭니다.

일반적으로 응용 프로그램에 오류가 발생하면 정리 작업을 여러 번 수행합니다. 그런 다음 사용자에게 오류를 알리고 문제 해결을 위한 옵션을 제공합니다.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

