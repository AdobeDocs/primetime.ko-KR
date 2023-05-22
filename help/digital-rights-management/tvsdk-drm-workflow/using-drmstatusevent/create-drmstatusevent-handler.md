---
title: DRMStatusEvent 처리기 만들기
description: DRMStatusEvent 처리기 만들기
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# DRMStatusEvent 처리기 만들기{#create-a-drmstatusevent-handler}

다음 예제에서는 이벤트를 발생시킨 Primetime 개체에 대한 DRM 콘텐츠 상태 정보를 출력하는 이벤트 처리기를 만듭니다.

보호된 콘텐츠를 가리키는 Primetime 개체에 이벤트 처리기를 추가합니다.

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

