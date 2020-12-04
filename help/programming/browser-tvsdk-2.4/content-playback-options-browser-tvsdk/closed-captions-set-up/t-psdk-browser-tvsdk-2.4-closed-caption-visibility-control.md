---
description: 자막의 가시성을 제어할 수 있습니다. 가시성이 켜지면 현재 선택한 트랙이 표시됩니다.
seo-description: 자막의 가시성을 제어할 수 있습니다. 가시성이 켜지면 현재 선택한 트랙이 표시됩니다.
seo-title: 자막 가시성 제어
title: 자막 가시성 제어
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 자막 표시 제어{#control-closed-caption-visibility}

자막의 가시성을 제어할 수 있습니다. 가시성이 켜지면 현재 선택한 트랙이 표시됩니다.

>[!TIP]
>
>현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.

플레이어가 검색 모드로 들어갈 때 닫힌 캡션 텍스트가 표시되는 경우 검색이 완료된 후 텍스트가 더 이상 표시되지 않습니다. 대신, 몇 초 후 Browser TVSDK는 마지막 검색 위치 이후 비디오에 다음 닫힌 캡션 텍스트를 표시합니다.

>[!TIP]
>
>닫힌 캡션의 가시성 값은 `MediaPlayer.VISIBLE` 및 `MediaPlayer.INVISIBLE`로 제어됩니다.

1. `MediaPlayer.ccVisibility` 속성을 사용하여 자막의 현재 가시성 설정에 액세스합니다.

