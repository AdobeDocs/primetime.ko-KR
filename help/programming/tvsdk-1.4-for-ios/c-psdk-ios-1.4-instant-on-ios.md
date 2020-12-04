---
description: Instant-on은 하나 이상의 채널에서 미디어 부분을 미리 로드합니다. 사용자가 채널을 선택하거나 전환하면 일부 버퍼링이 이미 완료되었기 때문에 컨텐츠가 더 빨리 시작됩니다.
seo-description: Instant-on은 하나 이상의 채널에서 미디어 부분을 미리 로드합니다. 사용자가 채널을 선택하거나 전환하면 일부 버퍼링이 이미 완료되었기 때문에 컨텐츠가 더 빨리 시작됩니다.
seo-title: 인스턴트 온
title: 인스턴트 온
uuid: 23864919-9045-4223-9e47-464e38ebe5ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Instant-on{#instant-on}

Instant-on은 하나 이상의 채널에서 미디어 부분을 미리 로드합니다. 사용자가 채널을 선택하거나 전환하면 일부 버퍼링이 이미 완료되었기 때문에 컨텐츠가 더 빨리 시작됩니다.

플레이어가 `PTMediaPlayerStatusReady` 상태인 경우 `prepareToPlay`을(를) 호출하여 나중에 재생할 수 있도록 일부 컨텐츠를 미리 로드하고 처리합니다.

>[!TIP]
>
>`prepareToPlay`을(를) 호출하지 않으면 `play`을(를) 호출하면 먼저 `prepareToPlay`가 호출됩니다. 현재 사전 로드 및 처리가 완료됩니다.

TVSDK는 `prepareToPlay`에 대해 다음 작업 중 일부 또는 전체를 완료합니다.

* 메타데이터 키 `kSyncCookiesWithAVAsset`이(가) 설정된 경우 TVSDK는 쿠키를 동기화하기 위해 원본 M3U8 파일에 한 번의 요청을 수행합니다.
* DRM 메타데이터 키를 로드합니다.
* 컨텐츠를 재생하는 데 필요한 일부 구조, 요소 또는 자산을 만들고 준비합니다.

>[!TIP]
>
>`PTMediaPlayer` 및 `PTMediaPlayerItem` `prepareToPlay` 메서드는 같습니다. 각 자산에 대해 별도의 `PTMediaPlayer` 인스턴스를 만들지 않으려면 `PTMediaPlayerItem` 메서드를 사용하십시오.

Instant-on을 사용하면 이러한 모든 인스턴스의 백그라운드 및 버퍼 비디오 스트림에서 동시에 여러 미디어 플레이어 인스턴스 또는 미디어 플레이어 항목 로더 인스턴스를 시작할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 `play`을(를) 호출하면 더 빨리 재생됩니다.
