---
description: 이러한 클래스는 광고, 네임스페이스 및 추적을 위한 메타데이터를 제공합니다.
title: 메타데이터 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 메타데이터 클래스{#metadata-classes}

이러한 클래스는 광고, 네임스페이스 및 추적을 위한 메타데이터를 제공합니다.

패키지: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 이름 | 설명 |
|---|---|
| [AdvertisingMeta](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 지정된 미디어 항목에 대한 광고를 해결하기 위해 구성해야 하는 속성을 제공하는 클래스입니다. 플레이어에서 광고를 성공적으로 확인하도록 구성하려면 필요한 속성을 모두 설정해야 합니다. |
| AuditudeMetadata | 사용하지 않음. AuditudeSettings를 사용합니다. |
| [Auditude 설정](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Java를 확장하는 클래스 `AdvertisingMetadata` 특히 구문에 사용됩니다. 지정된 미디어 항목에 대한 구문 광고를 해결하기 위해 구성할 속성을 제공합니다. 성공적으로 광고를 해결하도록 플레이어를 구성하려면 영역 ID, 미디어 ID 및 광고 서버 URL을 포함한 모든 필수 속성을 설정해야 합니다. |
| [메타데이터](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 플레이어에 사용할 수 있는 모든 메타데이터와 추가 개체를 구성하기 위한 일반 인터페이스를 정의합니다. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 임의의 키-값 쌍을 저장하기 위한 일반 데이터 구조와 같은 클래스입니다. |
| [TimedMeta](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 미디어 스트림에 삽입된 시간 메타데이터의 원시 표현에 대한 클래스입니다. |
