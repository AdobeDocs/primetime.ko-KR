---
description: TVSDK는 기본 또는 사용자 지정 태그가 발견되거나 매니페스트에서 재생 목록이 변경될 때마다 시간 메타데이터 이벤트를 전달하고 시간 메타데이터를 생성합니다. 이벤트는 매니페스트에 표시되는 순서대로 발송됩니다.
title: 시간 메타데이터 이벤트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 시간 메타데이터 이벤트{#timed-metadata-events}

TVSDK는 기본 또는 사용자 지정 태그가 발견되거나 매니페스트에서 재생 목록이 변경될 때마다 시간 메타데이터 이벤트를 전달하고 시간 메타데이터를 생성합니다. 이벤트는 매니페스트에 표시되는 순서대로 발송됩니다.

플레이어는 다음 이벤트를 기반으로 작업을 구현합니다.

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: ID3 시간 메타데이터가 처리될 때 발송됩니다.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: 시간 메타데이터가 처리되고 기회가 검색되지 않은 경우 발송됩니다.
