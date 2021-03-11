---
description: 관리자 팩터리를 사용하여 코드를 거치지 않고 기능을 켜거나 끌 수 있습니다.
title: ManagerFactory를 사용하여 기능 활성화 또는 비활성화
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# ManagerFactory{#turning-features-on-or-off-using-managerfactory} 사용 시 기능 켜기 또는 끄기

관리자 팩터리를 사용하여 코드를 거치지 않고 기능을 켜거나 끌 수 있습니다.

아래 예제의 역량 강화 인수는 기능의 사용 여부를 결정합니다. false이면 기능 관리자가 만들어지지만 기능 관리자가 생성되지 않은 것처럼 기본 기능만 플레이어에 제공합니다. true이면 기능 관리자가 만들어지고 기능이 활성화되며 미디어 플레이어는 구성 파일의 입력을 받습니다.

예를 들어 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 파일에서 다음을 수행합니다.

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API 설명서**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)