---
description: 인스턴트 온(Instant-on)은 하나 이상의 채널에서 미디어 일부를 미리 로드합니다. 사용자가 채널을 선택하거나 전환하면 일부 버퍼링이 이미 완료되었기 때문에 콘텐츠가 더 빨리 시작됩니다.
title: 즉시 사용
exl-id: 096104a7-867f-43e3-8433-f697d0224e21
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 즉시 사용 {#instant-on}

인스턴트 온(Instant-on)은 하나 이상의 채널에서 미디어 일부를 미리 로드합니다. 사용자가 채널을 선택하거나 전환하면 일부 버퍼링이 이미 완료되었기 때문에 콘텐츠가 더 빨리 시작됩니다.

플레이어가 다음에 있을 때 `PTMediaPlayerStatusReady` 상태, 호출 `prepareToPlay` 를 클릭하여 일부 컨텐츠를 미리 로드하고 나중에 재생할 수 있습니다.

>[!TIP]
>
>호출하지 않으면 `prepareToPlay`, 호출 `play` 자동 호출 `prepareToPlay` 첫 번째. 지금은 미리 로드 및 처리가 완료되었습니다.

TVSDK는에 대한 다음 작업의 일부 또는 전부를 완료합니다. `prepareToPlay`:

* 메타데이터 키인 경우 `kSyncCookiesWithAVAsset` 가 설정되면, TVSDK는 쿠키를 동기화하기 위해 원본 M3U8 파일에 대해 하나의 요청을 수행합니다.
* DRM 메타데이터 키를 로드합니다.
* 콘텐츠 재생에 필요한 일부 구조, 요소 또는 에셋을 만들고 준비합니다.

>[!TIP]
>
>다음 `PTMediaPlayer` 및 `PTMediaPlayerItem` `prepareToPlay` 메서드는 같습니다. 별도의 항목을 만들지 않으려면 `PTMediaPlayer` 각 에셋에 대한 인스턴스에서는 `PTMediaPlayerItem` 메서드를 사용합니다.

Instant-on을 사용하면 여러 미디어 플레이어 인스턴스 또는 미디어 플레이어 항목 로더 인스턴스를 동시에 배경에서 실행하고 이러한 모든 인스턴스에서 비디오 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 `play` 새 채널에서 더 빨리 재생이 시작됩니다.
