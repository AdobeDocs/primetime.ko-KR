---
description: 사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.
title: 사용자 정의 광고 마커 검색을 위한 재생 동작 제어
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 사용자 지정 광고 마커 검색 재생 동작 제어{#control-playback-behavior-for-seeking-over-custom-ad-markers}

사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.

기본적으로 사용자가 사용자 지정 광고 마커 배치로 인해 발생하는 광고 섹션을 검색하거나 지나치면 TVSDK는 광고를 건너뜁니다. 표준 광고 중단에 대한 현재 재생 비헤이비어와 다를 수 있습니다.

사용자가 하나 이상의 사용자 지정 광고를 지난 후 검색하는 경우 TV SDK에서 재생 헤드의 위치를 최근에 건너뛴 사용자 지정 광고 시작 부분으로 바꿀 수 있습니다.

1. `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 열거형이 문자열 값 &quot;true&quot;로 설정된 메타데이터 인스턴스를 구성합니다(부울 `true` 아님).

1. `MediaResource` 인스턴스를 만들고 구성하여 추가 구성 옵션을 `TimeRangeCollection.toMetadata`에 전달합니다. 이 메서드는 다른 일반 메타데이터 구조를 통해 추가 구성 옵션을 받습니다.

