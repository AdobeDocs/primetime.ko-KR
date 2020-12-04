---
description: Manager Factory를 사용하면 코드를 확인하지 않고 기능을 켜거나 끌 수 있습니다.
seo-description: Manager Factory를 사용하면 코드를 확인하지 않고 기능을 켜거나 끌 수 있습니다.
seo-title: ManagerFactory를 사용하여 기능 활성화 또는 비활성화
title: ManagerFactory를 사용하여 기능 활성화 또는 비활성화
uuid: 385c2707-95f7-4628-8d25-67731151cb6a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# ManagerFactory{#turning-features-on-or-off-using-managerfactory}를 사용하여 기능을 켜거나 끕니다.

Manager Factory를 사용하면 코드를 확인하지 않고 기능을 켜거나 끌 수 있습니다.

아래 예제의 활성 인수 인수는 기능을 사용할지 여부를 결정합니다. false이면 기능 관리자가 만들어지지만 기능 관리자가 생성되지 않은 것처럼 기본 기능만 플레이어에 제공합니다. true이면 기능 관리자가 만들어지고 기능이 활성화되며 미디어 플레이어에서 구성 파일의 입력을 수락합니다.

예를 들어 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 파일에서 다음을 수행합니다.

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API 설명서**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)