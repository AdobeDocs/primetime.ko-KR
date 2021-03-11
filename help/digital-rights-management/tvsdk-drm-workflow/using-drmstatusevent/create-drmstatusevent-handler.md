---
title: DRMStatusEvent 핸들러 만들기
description: DRMStatusEvent 핸들러 만들기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# DRMStatusEvent 핸들러 만들기{#create-a-drmstatusevent-handler}

다음 예제에서는 이벤트를 시작한 Primetime 개체의 DRM 콘텐츠 상태 정보를 출력하는 이벤트 핸들러를 만듭니다.

보호된 콘텐츠를 가리키는 Primetime 개체에 이벤트 핸들러를 추가합니다.

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

