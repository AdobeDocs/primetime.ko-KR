---
description: 자막의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.
seo-description: 자막의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.
seo-title: 자막 가시성 제어
title: 자막 가시성 제어
uuid: b9d48d70-2554-4948-8654-fa45093c3782
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 개요 {#control-closed-caption-visibility-overview}

자막의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.

>[!TIP]
>
>플레이어가 검색 모드를 시작할 때 닫힌 캡션 텍스트가 표시되는 경우 검색이 완료된 후 텍스트가 더 이상 표시되지 않습니다. 대신, 몇 초 후 TVSDK는 종료 검색 위치 후 비디오에 다음 닫힌 캡션 텍스트를 표시합니다.
>
>자막의 가시성 값은 에 정의되어 `MediaPlayer.Visibility`있습니다.>
>
```java>
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```>



1. READY 상태 `MediaPlayer` 이상을 기다립니다.

   자세한 내용은 ui-state-prepared-wait-for 을 참조하십시오.
1. 닫힌 캡션의 현재 가시성 설정을 가져오려면 에서 getter 메서드를 `MediaPlayer`사용합니다. 이 메서드는 가시성 값을 반환합니다.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 닫힌 캡션의 가시성을 변경하려면 setter 메서드를 사용하여 가시성 값을 에서 전달하십시오 `MediaPlayer.Visibility`.

   예:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```

