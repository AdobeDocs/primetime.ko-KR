---
description: FER(전체 이벤트 재생)은 라이브/DVR 에셋 역할을 하는 VOD 에셋이므로, 애플리케이션이 광고를 올바르게 배치할 수 있도록 조치를 취해야 합니다.
title: 전체 이벤트 재생에서 광고 활성화
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 전체 이벤트 재생에서 광고 활성화{#enable-ads-in-full-event-replay}

FER(전체 이벤트 재생)은 라이브/DVR 에셋 역할을 하는 VOD 에셋이므로, 애플리케이션이 광고를 올바르게 배치할 수 있도록 조치를 취해야 합니다.

라이브 콘텐츠의 경우, TVSDK는 매니페스트의 메타데이터/큐를 사용하여 광고를 배치할 위치를 결정합니다. 그러나 때로는 라이브/선형 콘텐츠가 VOD 콘텐츠와 유사할 수 있습니다. 예를 들어 라이브 컨텐츠가 완료되면 `EXT-X-ENDLIST` 태그가 라이브 매니페스트에 추가됩니다. HLS의 경우 `EXT-X-ENDLIST` 태그는 스트림이 VOD 스트림임을 의미합니다. TVSDK는 광고를 올바르게 삽입하기 위해 이 스트림을 일반 VOD 스트림과 자동으로 구분할 수 없습니다.

애플리케이션은 를 지정하여 콘텐츠가 라이브인지 VOD인지를 TVSDK에 알려주어야 합니다. `AdSignalingMode`.

FER 스트림의 경우, Adobe Primetime Ad Decisioning 서버는 재생을 시작하기 전에 타임라인에 삽입해야 하는 광고 브레이크 목록을 제공해서는 안 됩니다. 이는 VOD 콘텐츠의 일반적인 프로세스입니다. 대신, 다른 시그널링 모드를 지정하면 TVSDK가 FER 매니페스트에서 모든 큐 포인트를 읽고 각 큐 포인트에 대해 광고 서버로 이동하여 광고 브레이크를 요청합니다. 이 프로세스는 라이브/DVR 콘텐츠와 유사합니다.

큐 포인트와 연결된 각 요청 외에도 TVSDK는 프리롤 광고에 대한 추가 광고 요청을 만듭니다.

1. vCMS와 같은 외부 소스에서 사용해야 하는 신호 모드를 가져옵니다.
1. 광고 관련 메타데이터를 만듭니다.
1. 기본 동작을 덮어써야 하는 경우 `AdSignalingMode` 를 사용하여 `AdvertisingMetadata.setSignalingMode`.

   유효한 값은 다음과 같습니다. `DEFAULT, SERVER_MAP`, 및 `MANIFEST_CUES`.

   호출하기 전에 광고 신호 모드를 설정해야 합니다. `prepareToPlay`. TVSDK가 타임라인에서 광고를 확인하고 배치하면 광고 신호 모드에 대한 변경 사항이 무시됩니다. 다음을 만들 때 모드 설정 `AuditudeSettings` 개체.

1. 계속 재생합니다.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
