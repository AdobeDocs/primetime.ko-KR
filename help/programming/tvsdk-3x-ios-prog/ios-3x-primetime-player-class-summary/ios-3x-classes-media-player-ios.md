---
description: Primetime Player Objective-C API 를 사용하여 플레이어의 동작을 사용자 지정할 수 있습니다.
title: 미디어 플레이어 클래스
exl-id: b58efff0-2455-4db5-93a0-4624291dc526
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 미디어 플레이어 클래스 {#media-player-classes}

Primetime Player Objective-C API 를 사용하여 플레이어의 동작을 사용자 지정할 수 있습니다.

이러한 클래스는 미디어 플레이어와 해당 리소스에 대해 설명합니다.

| 클래스 | 설명 |
|---|---|
| PTABRControlParameters | 모든 적응형 비트 전송률 제어 매개 변수를 캡슐화합니다. 지원되는 매개 변수는 다음과 같습니다.<ul><li>최소 비트 전송률</li><li>maxBitRate</li><li>초기 비트 전송률</li></ul> |
| PTDefaultMediaPlayerClientFactory | TVSDK에서 PTMediaPlayerClientFactory의 기본 구현입니다. availablePTOopportunityResolver, PTContentResolver 및 PTAdPolicySelector 인스턴스를 제공합니다. |
| PTMediaPlayer | Primetime Player 프레임워크의 루트 구성 요소를 정의합니다.애플리케이션은 이 클래스의 인스턴스를 만들어 미디어를 재생합니다. 이 구성 요소는 알림을 발송하여 지정된 시간에 플레이어의 상태를 애플리케이션에 알립니다. |
| PTMediaPlayerClientFactory | 사용자 정의 미디어 플레이어 클라이언트 팩토리가 사용 가능한 PTOopportunityResolver , PTContentResolver 및 PTAdPolicySelector 인스턴스를 제공하기 위해 구현해야 하는 방법을 설명하는 프로토콜입니다. |
| PTMediaPlayerItem | 특정 오디오-비디오 미디어를 나타냅니다. |
| PTMediaPlayerView | Primetime Player 프레임워크의 보기 구성 요소를 관리합니다. |
| PTMediaProfile | 변형 재생 목록의 단일 스트림 프로필을 나타냅니다. |
| PTMediaSelectionOption | 다양한 언어 환경 설정, 접근성 요구 사항 또는 사용자 지정 애플리케이션 구성을 수용하는 시청각 미디어 리소스를 나타냅니다. 유효한 옵션 유형:<ul><li>자막(PTMediaSelectionOptionTypeSubtitle)</li><li>대체 오디오(PTMediaSelectionOptionTypeAudio)</li><li>폐쇄 캡션(PTMediaSelectionOptionTypeCC)</li><li>정의되지 않음(PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOopportunityResolver 클래스,PTOopportunityResolver 프로토콜 | Adobe Primetime 광고 결정 프로세스에 대한 배치로 사용될 매니페스트 내 큐 처리에 사용되는 클래스입니다. |
| PTOopportunityResolverDelegate | 사용자 지정 영업 기회 해결사( PTOopportunityResolver )가 영업 기회 해결 상태를 대리인에게 전달하는 데 사용해야 하는 방법을 설명하는 프로토콜입니다. |
| PTSDK | TVSDK 버전 및 해당 기능에 대해 설명합니다. |
| PTSDKConfig | TVSDK 전역 설정을 노출하고 애플리케이션에서 사용자 지정 HLS 태그를 구독할 수 있도록 합니다. |
| PTTextStyleRule | 규칙 사전을 구성하는 텍스트 스타일 속성 키를 나타내는 상수를 정의합니다. |
