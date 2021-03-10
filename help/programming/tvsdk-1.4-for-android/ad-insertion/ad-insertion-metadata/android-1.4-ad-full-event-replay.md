---
description: FER(Full-Event Replay)는 실시간/DVR 자산 역할을 하는 VOD 자산이므로 애플리케이션이 광고를 올바로 배치하도록 조치를 취해야 합니다.
title: 전체 이벤트 재생에서 광고 활성화
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# 전체 이벤트 재생에서 광고 활성화{#enable-ads-in-full-event-replay}

FER(Full-Event Replay)는 실시간/DVR 자산 역할을 하는 VOD 자산이므로 애플리케이션이 광고를 올바로 배치하도록 조치를 취해야 합니다.

라이브 콘텐츠의 경우 TVSDK는 매니페스트의 메타데이터/큐를 사용하여 광고를 배치할 위치를 결정합니다. 하지만 실시간/선형 컨텐츠가 VOD 컨텐츠와 비슷할 수도 있습니다. 예를 들어 라이브 콘텐츠가 완료되면 `EXT-X-ENDLIST` 태그가 라이브 매니페스트에 추가됩니다. HLS의 경우 `EXT-X-ENDLIST` 태그는 스트림이 VOD 스트림임을 의미합니다. TVSDK는 광고를 올바로 삽입하기 위해 일반 VOD 스트림과 이 스트림을 자동으로 구별할 수 없습니다.

응용 프로그램은 `AdSignalingMode`을(를) 지정하여 컨텐츠가 실시간 또는 VOD인지 TVSDK에 알려주어야 합니다.

FER 스트림의 경우 Adobe Primetime 광고 결정 서버는 재생을 시작하기 전에 타임라인에 삽입해야 하는 광고 중단 목록을 제공하지 않아야 합니다. VOD 컨텐츠의 일반적인 프로세스입니다. 대신 다른 신호 모드를 지정하여 TVSDK는 FER 매니페스트에서 모든 큐 포인트를 읽고 각 큐 포인트의 광고 서버로 이동하여 광고 중단을 요청합니다. 이 프로세스는 라이브/DVR 컨텐츠와 유사합니다.

TVSDK는 큐 포인트와 연관된 각 요청 이외에도 프리롤 광고에 대한 추가 광고 요청을 수행합니다.

1. vCMS와 같은 외부 소스에서 사용해야 하는 신호 모드를 가져옵니다.
1. 광고 관련 메타데이터를 만듭니다.
1. 기본 동작을 덮어써야 하는 경우 `AdvertisingMetadata.setSignalingMode`을(를) 사용하여 `AdSignalingMode`을(를) 지정합니다.

   유효한 값은 `DEFAULT, SERVER_MAP` 및 `MANIFEST_CUES`입니다.

   `prepareToPlay`을(를) 호출하기 전에 광고 신호 모드를 설정해야 합니다. TVSDK가 타임라인에서 광고를 확인하고 배치하기 시작하면 광고 신호 모드에 대한 변경 사항은 무시됩니다. `AuditudeSettings` 개체를 만들 때 모드를 설정합니다.

1. 계속 재생할 수 있습니다.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

