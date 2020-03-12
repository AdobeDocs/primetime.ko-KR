---
description: 비디오 분석 관리자 만들기
seo-description: 비디오 분석 관리자 만들기
seo-title: 비디오 분석 관리자 만들기
title: 비디오 분석 관리자 만들기
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 비디오 분석 관리자 만들기 {#create-the-video-analytics-manager}

새 관리자 클래스( `VAManager`)가 Android 참조 구현에 추가되었습니다. `VAManager` 간단하게 `VideoHeartbeat` 클래스의 인스턴스를 만들고 삭제합니다. 참조 구현은 새 인스턴스를 만들 때 `VAManager` 인스턴스를 만들고, 인스턴스가 `MediaPlayer` `MediaPlayer` 삭제될 때 해당 인스턴스를 삭제합니다. 이 기능은 에서 구현됩니다 `PlayerFragment.java`.

## 새 비디오 분석 관리자를 만들려면

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

config 변수는 구체적인 구현 `IVAConfig` 방법이며 런타임 `VideoHeartbeat` 구성을 포함합니다.

>[!NOTE]
>
>Android 응용 프로그램이 Adobe Analytics 계정으로 구성되지 않은 경우, 인스턴스가 만들어지고 활성화된 경우에도 비디오 추적 데이터가 생성되지 `VAManager` 않습니다.

