---
description: 닫힘 캡션의 가시성을 제어할 수 있습니다. 가시성이 켜져 있으면 현재 선택한 트랙이 표시됩니다.
title: 닫힌 캡션 표시 제어
exl-id: e74c0344-43f3-4ed7-bbf2-d89dd3df8a33
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 닫힌 캡션 표시 제어{#control-closed-caption-visibility}

닫힘 캡션의 가시성을 제어할 수 있습니다. 가시성이 켜져 있으면 현재 선택한 트랙이 표시됩니다.

>[!TIP]
>
>현재 트랙을 변경하는 경우 가시성 설정은 동일하게 유지됩니다.

플레이어가 찾기 모드에 들어갈 때 닫힌 캡션 텍스트가 표시되면 찾기가 완료된 후 텍스트가 더 이상 표시되지 않습니다. 대신, 몇 초 후에 Browser TVSDK는 찾기 종료 위치 후에 비디오에 다음 자막 텍스트를 표시합니다.

>[!TIP]
>
>폐쇄 캡션의 가시성 값은 `MediaPlayer.VISIBLE` 및 `MediaPlayer.INVISIBLE`.

1. 사용 `MediaPlayer.ccVisibility` 속성을 사용하여 폐쇄 캡션의 현재 가시성 설정에 액세스할 수 있습니다.
