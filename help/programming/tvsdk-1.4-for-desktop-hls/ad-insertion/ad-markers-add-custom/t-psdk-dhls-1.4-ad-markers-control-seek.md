---
description: 사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 찾는 방법에 대한 기본 동작을 재정의할 수 있습니다.
title: 사용자 지정 광고 마커를 통한 찾기를 위한 재생 비헤이비어 제어
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 사용자 지정 광고 마커를 통한 찾기를 위한 재생 비헤이비어 제어{#control-playback-behavior-for-seeking-over-custom-ad-markers}

사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 찾는 방법에 대한 기본 동작을 재정의할 수 있습니다.

기본적으로 사용자가 사용자 지정 광고 마커의 배치로 인해 발생하는 광고 섹션을 찾거나 지나가면 TVSDK가 광고를 건너뜁니다. 표준 광고 브레이크의 현재 재생 비헤이비어와 다를 수 있습니다.

사용자가 하나 이상의 사용자 지정 광고를 검색하면 가장 최근에 건너뛴 사용자 지정 광고의 시작으로 플레이헤드의 위치를 조정하도록 TVSDK에 지시할 수 있습니다.

1. 를 사용하여 메타데이터 인스턴스 구성 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 문자열 값 &quot;true&quot;로 설정된 열거형(부울이 아님) `true`).

1. 만들기 및 구성 `MediaResource` 인스턴스, 추가 구성 옵션을 로 전달 `TimeRangeCollection.toMetadata`. 이 방법은 다른 일반 메타데이터 구조를 통해 추가 구성 옵션을 받습니다.
