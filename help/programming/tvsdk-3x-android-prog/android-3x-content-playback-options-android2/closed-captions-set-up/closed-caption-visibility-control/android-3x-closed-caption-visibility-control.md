---
description: 자막의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.
seo-description: 자막의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.
seo-title: 자막 가시성 제어
title: 자막 가시성 제어
uuid: f142e60d-5581-4d1c-9d4d-a4a58ac1b67b
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# 자막 가시성 제어 {#control-closed-caption-visibility}

자막의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.

>[!TIP]
>
>플레이어가 검색 모드에 들어갈 때 닫힌 캡션 텍스트가 표시되는 경우 검색이 완료된 후 텍스트가 더 이상 표시되지 않습니다. 대신, 몇 초 후 TVSDK는 마지막 검색 위치 이후 비디오에 다음 닫힌 캡션 텍스트를 표시합니다.
>
>닫힌 캡션의 가시성 값은 에 정의되어 있습니다 `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 최소 준비 상태 `MediaPlayer` 에 있을 때까지 기다립니다. 자세한 내용은 [유효한 상태](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md)대기

1. 닫힌 캡션에 대한 현재 가시성 설정을 얻으려면 가시성 값을 반환하는 getter 방법 `MediaPlayer`을 사용하십시오.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 닫힌 캡션의 가시성을 변경하려면 setter 메서드를 사용하여 가시성 값을 전달하십시오 `MediaPlayer.Visibility`.

   예:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
