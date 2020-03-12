---
seo-title: DRMStatusEvent 핸들러 만들기
title: DRMStatusEvent 핸들러 만들기
uuid: 64f539d9-344c-4372-88b8-c8d098af9dd8
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# DRMStatusEvent 핸들러 만들기{#create-a-drmstatusevent-handler}

다음 예제에서는 이벤트를 시작한 Primetime 개체에 대한 DRM 콘텐츠 상태 정보를 출력하는 이벤트 핸들러를 만듭니다.

보호된 콘텐츠를 가리키는 Primetime 개체에 이벤트 핸들러를 추가합니다.

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

