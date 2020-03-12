---
description: 사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.
seo-description: 사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.
seo-title: 사용자 정의 광고 마커 검색을 위한 재생 동작 제어
title: 사용자 정의 광고 마커 검색을 위한 재생 동작 제어
uuid: 926299c6-9c23-457d-b836-08432e4e169e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 사용자 정의 광고 마커 검색을 위한 재생 동작 제어{#control-playback-behavior-for-seeking-over-custom-ad-markers}

사용자 지정 광고 마커를 사용할 때 TVSDK가 광고를 검색하는 방법에 대한 기본 동작을 재정의할 수 있습니다.

기본적으로 사용자가 사용자 지정 광고 마커를 배치하여 발생하는 광고 섹션을 검색하거나 지난 경우 TVSDK는 광고를 건너뜁니다. 표준 광고 중단에 대한 현재 재생 동작과 다를 수 있습니다.

사용자가 하나 이상의 사용자 지정 광고를 지난 경우 TVSDK에서 재생 헤드의 위치를 가장 최근에 건너뛴 사용자 지정 광고 시작 부분으로 변경하도록 지시할 수 있습니다.

1. 열거형이 &quot;true&quot;(부울이 아닌) 문자열 값으로 설정된 메타데이터 인스턴스를 구성합니다 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` `true`.

1. 추가 구성 옵션을 전달하여 `MediaResource` 인스턴스를 만들고 구성합니다 `TimeRangeCollection.toMetadata`. 이 메서드는 다른 일반 메타데이터 구조를 통해 추가 구성 옵션을 받습니다.

