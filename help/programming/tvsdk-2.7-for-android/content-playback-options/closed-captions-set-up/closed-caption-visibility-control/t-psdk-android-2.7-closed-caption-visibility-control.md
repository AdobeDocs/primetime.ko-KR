---
description: 닫힘 캡션의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하는 경우 가시성 설정은 동일하게 유지됩니다.
title: 닫힌 캡션 표시 제어
exl-id: 358e32d8-7a3b-42bd-900b-dafe8eae3edf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 개요 {#control-closed-caption-visibility-overview}

닫힘 캡션의 가시성을 제어할 수 있습니다. 가시성이 활성화되면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하는 경우 가시성 설정은 동일하게 유지됩니다.

>[!TIP]
>
>플레이어가 찾기 모드에 들어갈 때 닫힌 캡션 텍스트가 표시되면 찾기가 완료된 후 텍스트가 더 이상 표시되지 않습니다. 대신, 몇 초 후에 TVSDK는 종료 탐색 위치 후에 비디오에 다음 자막 텍스트를 표시합니다.
>
>폐쇄 캡션의 가시성 값은에 정의되어 있습니다. `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 다음을 기다리십시오. `MediaPlayer` 적어도 준비됨 상태여야 합니다.

   자세한 내용은 ui-state-prepared-wait-for 를 참조하십시오.
1. 닫힘 캡션에 대한 현재 가시성 설정을 가져오려면 `MediaPlayer`- 가시성 값을 반환합니다.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 닫힘 캡션의 가시성을 변경하려면 setter 메서드를 사용하여 가시성 값을 다음 위치에 전달합니다. `MediaPlayer.Visibility`.

   예:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
