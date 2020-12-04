---
description: 대부분의 TVSDK 플레이어 방법을 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
seo-description: 대부분의 TVSDK 플레이어 방법을 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
seo-title: 유효한 상태 대기
title: 유효한 상태 대기
uuid: ad9df366-c443-4e6b-a7ab-658d5691eb94
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 유효한 상태 {#wait-for-a-valid-state}을(를) 기다리는 중

대부분의 TVSDK 플레이어 방법을 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

플레이어가 다양한 상태를 따라 이동합니다. 플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필수 상태가 아닌 경우 많은 플레이어 메서드에서 `IllegalStateException`을(를) throw합니다.

필요한 상태는 보통 `PTMediaPlayerStatusReady`입니다.