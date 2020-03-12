---
description: 이러한 클래스는 광고, 네임스페이스 및 추적을 위한 메타데이터를 제공합니다.
seo-description: 이러한 클래스는 광고, 네임스페이스 및 추적을 위한 메타데이터를 제공합니다.
seo-title: 메타데이터 클래스
title: 메타데이터 클래스
uuid: 6d5099c8-d562-4635-9ef0-068cc6fb9f82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 메타데이터 클래스{#metadata-classes}

이러한 클래스는 광고, 네임스페이스 및 추적을 위한 메타데이터를 제공합니다.

패키지: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 이름 | 설명 |
|---|---|
| [광고 메타데이터](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 지정된 미디어 항목에 대한 광고를 해결하기 위해 구성해야 하는 속성을 제공하는 클래스입니다. 광고를 성공적으로 해결하기 위해 플레이어를 구성하려면 필요한 모든 속성을 설정해야 합니다. |
| AuditudeMetadata | 가치 하락. AuditudeSettings를 사용합니다. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 구문에 `AdvertisingMetadata` 대해 Java를 확장하는 클래스입니다. 지정된 미디어 항목에 대한 구문 광고를 해결하기 위해 구성할 속성을 제공합니다. 광고를 성공적으로 해결하기 위해 플레이어를 구성하려면 영역 ID, 미디어 ID 및 광고 서버 URL을 비롯한 모든 필수 속성을 설정해야 합니다. |
| [메타데이터](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 플레이어와 추가 개체에 대해 사용 가능한 모든 메타데이터를 구성하기 위한 일반 인터페이스를 정의합니다. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 임의의 키-값 쌍을 저장하기 위한 일반적인 데이터 구조 비슷한 클래스입니다. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 미디어 스트림에 삽입된 시간 메타데이터의 원시 표현을 위한 클래스입니다. |