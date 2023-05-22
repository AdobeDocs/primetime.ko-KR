---
description: 대체 오디오 기능 관리자를 만들어 지연 바인딩 또는 대체 오디오 스트림을 플레이어에 통합할 수 있습니다.
title: 지연 바인딩 오디오 통합
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 지연 바인딩 오디오 통합 {#integrate-late-binding-audio}

대체 오디오 기능 관리자를 만들어 지연 바인딩 또는 대체 오디오 스트림을 플레이어에 통합할 수 있습니다.

* 대체 오디오 관리자를 만들려면 다음 작업을 수행하십시오.

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* ManagerFactory를 사용하여 대체 오디오를 활성화하려면 다음 코드 줄이 `PlayerFragment.java` 파일:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   대체 오디오를 비활성화하려면:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```
