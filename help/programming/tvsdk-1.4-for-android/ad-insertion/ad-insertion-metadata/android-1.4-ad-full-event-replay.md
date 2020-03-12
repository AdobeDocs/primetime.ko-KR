---
description: FER(Full-Event Replay)는 실시간/DVR 자산 역할을 하는 VOD 자산이므로 애플리케이션이 광고가 올바르게 배치되도록 조치를 취해야 합니다.
seo-description: FER(Full-Event Replay)는 실시간/DVR 자산 역할을 하는 VOD 자산이므로 애플리케이션이 광고가 올바르게 배치되도록 조치를 취해야 합니다.
seo-title: 전체 이벤트 재생에서 광고 활성화
title: 전체 이벤트 재생에서 광고 활성화
uuid: 70e463bd-332c-4f91-ac05-03e79c0939a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 전체 이벤트 재생에서 광고 활성화{#enable-ads-in-full-event-replay}

FER(Full-Event Replay)는 실시간/DVR 자산 역할을 하는 VOD 자산이므로 애플리케이션이 광고가 올바르게 배치되도록 조치를 취해야 합니다.

라이브 콘텐츠의 경우 TVSDK는 매니페스트의 메타데이터/큐를 사용하여 광고를 배치할 위치를 결정합니다. 그러나 실시간/선형 컨텐츠는 VOD 컨텐츠와 유사할 수 있습니다. 예를 들어 라이브 컨텐츠가 완료되면 `EXT-X-ENDLIST` 태그가 라이브 매니페스트에 추가됩니다. HLS의 경우 `EXT-X-ENDLIST` 태그는 스트림이 VOD 스트림임을 의미합니다. TVSDK는 이 스트림을 일반 VOD 스트림과 자동으로 구별하여 광고를 올바로 삽입할 수 없습니다.

애플리케이션은 컨텐츠를 지정하여 TVSDK에 컨텐츠의 실시간 또는 VOD를 알려주어야 `AdSignalingMode`합니다.

FER 스트림의 경우 Adobe Primetime 광고 결정 서버는 재생을 시작하기 전에 타임라인에 삽입해야 하는 광고 중단 목록을 제공하지 않아야 합니다. VOD 컨텐츠의 일반적인 프로세스입니다. 대신 다른 신호 모드를 지정하여 TVSDK는 FER 매니페스트에서 모든 큐 포인트를 읽고 각 큐 포인트에 대한 광고 서버로 이동하여 광고 중단을 요청합니다. 이 프로세스는 라이브/DVR 컨텐츠와 유사합니다.

TVSDK는 큐 포인트와 연결된 각 요청 외에도 프리롤 광고에 대한 추가 광고 요청을 수행합니다.

1. vCMS와 같은 외부 소스에서 사용해야 하는 신호 모드를 얻습니다.
1. 광고 관련 메타데이터를 만듭니다.
1. 기본 동작을 덮어써야 하는 경우 를 `AdSignalingMode` 사용하여 지정합니다 `AdvertisingMetadata.setSignalingMode`.

   유효한 값은 `DEFAULT, SERVER_MAP`및 `MANIFEST_CUES`입니다.

   호출하기 전에 광고 신호 모드를 설정해야 합니다 `prepareToPlay`. TVSDK가 타임라인에서 광고를 확인하고 배치하기 시작하면 광고 신호 모드로 변경된 내용은 무시됩니다. 객체를 만들 때 모드를 `AuditudeSettings` 설정합니다.

1. 계속 재생할 수 있습니다.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

