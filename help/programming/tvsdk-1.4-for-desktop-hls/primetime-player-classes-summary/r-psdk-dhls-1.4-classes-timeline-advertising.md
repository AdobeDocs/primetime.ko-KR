---
description: 이러한 클래스는 타임라인 내에서 발생하는 광고에 대한 정보를 제공합니다.
title: 타임라인 광고 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 타임라인 광고 클래스 {#timeline-advertising-classes}

이러한 클래스는 타임라인 내에서 발생하는 광고에 대한 정보를 제공합니다.

패키지: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
패키지: [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| 이름 | 설명 |
|---|---|
| [광고](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | 광고 추상화를 정의하고 모든 광고 정보를 보유하는 클래스입니다. 고유한 ID, 기간 및 `MediaResource`. 다음 `MediaResource` 실제 광고 콘텐츠가 있는 URL을 포함합니다. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | 표시할 자산을 나타내는 클래스입니다. 광고 자산을 나타내는 클래스입니다. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | 재생 중 특정 시점에 재생되는 여러 광고에 대한 통합 보기를 제공하는 클래스입니다. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | 사용자가 검색하는 동안 광고를 우회하는 것과 관련된 광고 재생 정책을 정의하는 열거형입니다. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | 특정 광고 브레이크와 연결된 타임라인 항목입니다. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | 광고 브레이크를 시청한 것으로 표시할 시기에 대한 가능한 정책에 대한 열거형 클래스입니다. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | 자산과 연결된 클릭 인스턴스를 나타내는 클래스입니다. 이 인스턴스에는 사용자에게 추가 정보를 제공하는 데 사용할 수 있는 클릭스루 URL 및 제목에 대한 정보가 포함되어 있습니다. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | 검색 또는 트릭 플레이 모드 후 광고 브레이크 재생을 재개할 위치에 대한 가능한 정책에 대한 열거형 클래스입니다. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | 찾기 또는 일반 재생과 같이 플레이어가 재생되는 방법을 나열하는 열거형 클래스입니다. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 의 속성을 정의하는 인터페이스 `AdPolicySelector` API 호출. 이러한 속성은 각 광고 동작을 적용하기 위한 컨텍스트를 제공합니다. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | 광고 동작을 적용하기 위한 광고 정책 선택기 인터페이스입니다. 응용 프로그램은 필요한 모든 메서드를 구현하거나 기존 기본 정책 선택기 클래스를 확장하여 특정 동작을 사용자 지정하여 이 인터페이스를 준수할 수 있습니다. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | 특정 광고와 연계된 타임라인 항목. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | TVSDK 프로세스에서 primetime 광고 해결을 처리하는 클래스입니다. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | TVSDK에서 지원하는 모든 광고 유형을 열거합니다. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | 클래스. |
