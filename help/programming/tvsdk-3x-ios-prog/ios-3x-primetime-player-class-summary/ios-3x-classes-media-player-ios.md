---
description: Primetime Player Objective-C API를 사용하여 플레이어의 비헤이비어를 사용자 정의할 수 있습니다.
title: 미디어 플레이어 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# 미디어 플레이어 클래스 {#media-player-classes}

Primetime Player Objective-C API를 사용하여 플레이어의 비헤이비어를 사용자 정의할 수 있습니다.

이러한 클래스는 미디어 플레이어 및 해당 리소스를 설명합니다.

| 클래스 | 설명 |
|---|---|
| PTABRControlParameters | 모든 적응형 비트 전송률 제어 매개 변수를 캡슐화합니다. 지원되는 매개 변수는 다음과 같습니다.<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | TVSDK에서 PTMediaPlayerClientFactors의 기본 구현. availablePTOpportunityResolver, PTContentResolver 및PTAdPolicySelector 인스턴스를 제공합니다. |
| PTMediaPlayer | Primetime Player 프레임워크의 루트 구성 요소를 정의합니다. 응용 프로그램은 미디어를 재생하기 위해 이 클래스의 인스턴스를 만듭니다. 이 구성 요소는 알림을 전달하여 응용 프로그램에서 지정된 시간에 플레이어 상태를 알 수 있도록 합니다. |
| PTMediaPlayerClientFactory | 사용 가능한 PTOpportunityResolver, PTContentResolver 및 PTAdPolicySelector 인스턴스를 제공하기 위해 사용자 정의 미디어 플레이어 클라이언트 팩터리가 구현해야 하는 방법을 설명하는 프로토콜입니다. |
| PTMediaPlayerItem | 특정 오디오 비디오 미디어를 나타냅니다. |
| PTMediaPlayerView | Primetime Player 프레임워크의 보기 구성 요소를 관리합니다. |
| PTMediaProfile | 변형 재생 목록에서 단일 스트림의 프로파일을 나타냅니다. |
| PTMediaSelectionOption | 서로 다른 언어 환경 설정, 액세서빌러티 요구 사항 또는 사용자 정의 응용 프로그램 구성을 수용하기 위한 오디오 비주얼 미디어 리소스를 나타냅니다. 유효한 옵션 유형:<ul><li>자막(PTMediaSelectionOptionTypeSubtitle)</li><li>대체 오디오(PTMediaSelectionOptionTypeAudio)</li><li>자막(PTMediaSelectionOptionTypeCC)</li><li>정의되지 않음(PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver 클래스,PTOpportunityResolver 프로토콜 | Adobe Primetime 광고 결정 프로세스를 위한 배열로 사용될 매니페스트 내 큐를 처리하는 데 사용되는 클래스입니다. |
| PTOpportunityResolverDelegate | 사용자 지정 기회 해결 프로그램( PTOpportunityResolver )이 기회 해결 상태를 대리인에게 알리는 데 사용해야 하는 방법을 설명하는 프로토콜입니다. |
| PTSDK | TVSDK 버전 및 기능에 대해 설명합니다. |
| PTSDKConfig | TVSDK 전역 설정을 표시하고 응용 프로그램이 사용자 정의 HLS 태그에 가입할 수 있도록 합니다. |
| PTTextStyleRule | 규칙 사전을 구성하는 텍스트 스타일 속성 키를 나타내는 상수를 정의합니다. |
