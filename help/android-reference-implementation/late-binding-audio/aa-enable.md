---
description: 대체 오디오 기능 관리자를 만들어 지연 바인딩 또는 대체 오디오 스트림을 플레이어에 통합할 수 있습니다.
seo-description: 대체 오디오 기능 관리자를 만들어 지연 바인딩 또는 대체 오디오 스트림을 플레이어에 통합할 수 있습니다.
seo-title: 지연 바인딩 오디오 통합
title: 지연 바인딩 오디오 통합
uuid: cd2e259a-2af4-4d7b-a856-79bd087e8ca6
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 지연 바인딩 오디오 {#integrate-late-binding-audio} 통합

대체 오디오 기능 관리자를 만들어 지연 바인딩 또는 대체 오디오 스트림을 플레이어에 통합할 수 있습니다.

* 대체 오디오 관리자를 만들려면:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* ManagerFactory를 사용하여 대체 오디오를 활성화하려면 다음 코드 줄이 `PlayerFragment.java` 파일에 있는지 확인하십시오.

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   대체 오디오를 비활성화하려면

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

