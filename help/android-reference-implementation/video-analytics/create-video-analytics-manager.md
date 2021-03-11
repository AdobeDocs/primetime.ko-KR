---
description: 비디오 분석 관리자 만들기
title: 비디오 분석 관리자 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# 비디오 분석 관리자 {#create-the-video-analytics-manager} 만들기

새 관리자 클래스( `VAManager`)가 Android 참조 구현에 추가되었습니다. `VAManager` 클래스의 인스턴스를 만들고  `VideoHeartbeat` 파괴하면 됩니다. 참조 구현은 새 `MediaPlayer`을(를) 만들 때 `VAManager` 인스턴스를 만들고 `MediaPlayer`을(를) 삭제할 때 해당 인스턴스를 삭제합니다. 이것은 `PlayerFragment.java`에 구현됩니다.

## 새 비디오 분석 관리자를 만들려면

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config 변수는 `IVAConfig`의 구체적인 구현이며 런타임 `VideoHeartbeat` 구성을 포함합니다.

>[!NOTE]
>
>Android 응용 프로그램이 Adobe Analytics 계정으로 구성되지 않은 경우 `VAManager` 인스턴스가 만들어지고 활성화된 경우에도 비디오 추적 데이터가 생성되지 않습니다.

