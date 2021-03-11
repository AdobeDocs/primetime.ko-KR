---
description: 이러한 클래스는 타임라인 내에서 발생하는 광고에 대한 정보를 제공합니다.
title: 타임라인 광고 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# 타임라인 광고 클래스{#timeline-advertising-classes}

이러한 클래스는 타임라인 내에서 발생하는 광고에 대한 정보를 제공합니다.

패키지:[com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

패키지:[com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| 이름 | 설명 |
|--- |--- |
| [광고](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 광고 추상화를 정의하고 모든 광고 정보를 포함하는 클래스입니다. 고유 ID, 기간 및 `MediaResource`으로 정의됩니다. `MediaResource`에는 실제 광고 컨텐츠가 있는 URL이 포함되어 있습니다. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 표시할 자산을 나타내는 클래스입니다. 광고 자산을 나타내는 클래스입니다. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 재생하는 동안 특정 시점에 재생되는 여러 광고에 대한 통합 보기를 제공하는 클래스입니다. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | 광고 분리 배치 작업 클래스입니다. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | 검색하는 동안 광고를 건너뛰기 위한 사용자와 관련된 광고 재생 정책을 정의하는 열거형입니다. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 자산과 연결된 클릭 인스턴스를 나타내는 클래스입니다. 이 인스턴스에는 사용자에게 추가 정보를 제공하는 데 사용할 수 있는 클릭스루 URL과 제목에 대한 정보가 포함되어 있습니다. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | AdPolicySelector API 호출에 대한 속성을 정의하는 인터페이스입니다. 이러한 속성은 각 광고 동작을 적용하기 위한 컨텍스트를 제공합니다. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | 광고 행동을 적용하기 위한 광고 정책 선택기 인터페이스입니다. 애플리케이션은 필요한 모든 메서드를 구현하거나 기존 기본 정책 선택기 클래스를 확장하여 특정 비헤이비어를 사용자 정의할 수 있으므로 이 인터페이스에 맞출 수 있습니다. |
| `auditude.AuditudeAdProvider` | 사용되지 않습니다. AuditudeResolver를 사용합니다. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | 구문 프로세스에서 primetime 및 해결 방법을 처리하는 클래스입니다. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | ContentTracker 인터페이스를 구현하고 Primetime 광고 추적 이벤트를 정의하는 클래스입니다. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | 구문 프로세스에서 광고 해결 부분을 처리하는 클래스입니다. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | 라이브러리 또는 사용자 지정 광고 추적기와 통합하도록 설계된 광고 추적 모듈을 만들려면 구현해야 하는 프로토콜을 정의하는 인터페이스입니다. 이 인터페이스를 사용하려면 광고 진행 이벤트가 원격 광고 추적 시스템에 보고되는 방식을 정의해야 합니다. |
| [배치 정보](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | 배치 정보 요청을 추상화하는 클래스입니다. 해결된 각 광고에는 하나의 배치 정보가 첨부되어야 합니다. 배치 정보는 타임라인에서 광고가 배치되는 위치를 설명합니다. 여기에는 다음과 같은 정보가 포함됩니다. <ul><li>배치 위치(ms) </li><li>배치 유형(프리롤, 미드롤 또는 포스트롤) </li><li>교체할 기본 컨텐츠 청크의 지속 시간</li></ul> |
