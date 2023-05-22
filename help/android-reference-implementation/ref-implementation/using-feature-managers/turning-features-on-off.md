---
description: 관리자 팩토리를 사용하여 코드를 거치지 않고 기능을 켜거나 끌 수 있습니다.
title: ManagerFactory를 사용하여 기능 설정 또는 해제
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# ManagerFactory를 사용하여 기능 설정 또는 해제{#turning-features-on-or-off-using-managerfactory}

관리자 팩토리를 사용하여 코드를 거치지 않고 기능을 켜거나 끌 수 있습니다.

아래 예제의 지원 인수는 기능의 사용 여부를 결정합니다. false인 경우 피쳐 매니저가 생성되지만 피쳐 매니저가 생성되지 않은 것처럼 플레이어에 기본 기능만 제공합니다. true이면 기능 관리자가 생성되고 기능이 활성화되고 미디어 플레이어가 구성 파일의 입력을 받아들입니다.

예를 들어, `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 파일:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API 설명서**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
