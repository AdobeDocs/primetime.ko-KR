---
description: Video Analytics 관리자 만들기
title: Video Analytics 관리자 만들기
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Video Analytics 관리자 만들기 {#create-the-video-analytics-manager}

새 관리자 클래스( `VAManager`)이 Android 참조 구현에 추가되었습니다. `VAManager` 의 인스턴스를 단순히 만들고 소멸시킵니다. `VideoHeartbeat` 클래스. 참조 구현은 `VAManager` 인스턴스: 새로 만들기 `MediaPlayer` 이(가) 만들어지고 `MediaPlayer` 이(가) 파괴되었습니다. 다음에서 구현됩니다. `PlayerFragment.java`.

## 새 Video Analytics 관리자를 만들려면

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

구성 변수는 의 구체적인 구현입니다 `IVAConfig` 및 에는 런타임이 포함됩니다 `VideoHeartbeat` 구성.

>[!NOTE]
>
>Android 애플리케이션이 Adobe Analytics 계정으로 구성되어 있지 않으면 의 인스턴스라도 비디오 추적 데이터가 생성되지 않습니다. `VAManager` 이(가) 만들어지고 활성화됩니다.
