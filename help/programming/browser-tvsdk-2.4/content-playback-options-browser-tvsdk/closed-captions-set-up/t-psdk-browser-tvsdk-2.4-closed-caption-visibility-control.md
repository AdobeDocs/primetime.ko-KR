---
description: 닫힌 캡션의 가시성을 제어할 수 있습니다. 가시성이 설정되어 있으면 현재 선택된 트랙이 표시됩니다.
title: 자막 가시성 제어
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 닫힌 캡션 표시 제어{#control-closed-caption-visibility}

닫힌 캡션의 가시성을 제어할 수 있습니다. 가시성이 설정되어 있으면 현재 선택된 트랙이 표시됩니다.

>[!TIP]
>
>현재 트랙을 변경하면 가시성 설정이 동일하게 유지됩니다.

플레이어가 검색 모드로 들어갈 때 닫힌 캡션 텍스트가 표시되는 경우 검색이 완료된 후 텍스트가 표시되는 문제가 해결되었습니다. 대신, 몇 초 후 브라우저 TV는 종료 검색 위치 뒤에 비디오에 다음 닫힌 캡션 텍스트를 표시합니다.

>[!TIP]
>
>닫힌 캡션의 가시성 값은 `MediaPlayer.VISIBLE` 및 `MediaPlayer.INVISIBLE`로 제어됩니다.

1. `MediaPlayer.ccVisibility` 속성을 사용하여 닫힌 캡션의 현재 가시성 설정에 액세스합니다.

