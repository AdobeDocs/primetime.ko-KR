---
description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
title: 유효한 상태 대기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 유효한 상태{#wait-for-a-valid-state}을(를) 기다립니다.

대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

플레이어는 다양한 상태를 따라 이동합니다. 플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필요한 상태 이상이 아니면 많은 플레이어 메서드에서 `IllegalStateException`을(를) throw합니다.

필요한 상태는 보통 `PTMediaPlayerStatusReady`입니다.
