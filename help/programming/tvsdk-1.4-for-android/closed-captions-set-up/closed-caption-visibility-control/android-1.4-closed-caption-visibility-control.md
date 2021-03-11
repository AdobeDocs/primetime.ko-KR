---
description: 닫힌 캡션의 가시성을 제어할 수 있습니다. 가시성이 설정되어 있으면 현재 선택된 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.
title: 자막 가시성 제어
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 개요 {#control-closed-caption-visibility}

닫힌 캡션의 가시성을 제어할 수 있습니다. 가시성이 설정되어 있으면 현재 선택된 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.

>[!TIP]
>
>플레이어가 검색 모드로 들어갈 때 닫힌 캡션 텍스트가 표시되는 경우 검색이 완료된 후 텍스트가 표시되는 문제가 해결되었습니다. 대신, 몇 초 후 TVSDK는 끝 검색 위치 뒤에 비디오에 다음 닫힌 캡션 텍스트를 표시합니다.

>[!NOTE]
>
>닫힌 캡션의 가시성 값은 `MediaPlayer.Visibility`에 정의됩니다.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. MediaPlayer가 PREPARED 상태 이상을 가질 때까지 기다립니다( [유효한 상태](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md) 대기 참조).
1. 닫힌 캡션의 현재 가시성 설정을 가져오려면 가시성 값을 반환하는 MediaPlayer의 getter 메서드를 사용합니다.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. 닫힌 캡션의 가시성을 변경하려면 setter 메서드를 사용하여 `MediaPlayer.Visibility`의 가시성 값을 전달합니다.

   예:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

