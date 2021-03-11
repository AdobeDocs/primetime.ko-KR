---
description: TVSDK는 메서드, 메타데이터 및 알림을 비롯한 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.
title: 일시 중단 API 요소
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# 일시 중단 API 요소{#blackout-api-elements}

TVSDK는 메서드, 메타데이터 및 알림을 비롯한 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.

플레이어에서 일시 중단 솔루션을 구현할 때 다음을 사용할 수 있습니다.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 현재 로드된 리소스를 배경 리소스로 저장합니다. 이 메서드 후에 `replaceCurrentResource`이(가) 호출되면 TVSDK는 `unregisterCurrentBackgroundItem`을(를) 호출할 때까지 백그라운드 항목의 매니페스트를 계속 다운로드합니다.

   * `unregisterCurrentBackgroundItem`  현재 설정된 백그라운드 리소스를 삭제하고 배경 매니페스트를 가져오고 파싱하지 않습니다.

* **BlacketMetadata** 일시 중단과 관련된 메타데이터 유형입니다.

   이렇게 하면 TVSDK에서 볼 수 없는 범위(추가 `TimeRange` 속성(`nonseekableRange`)를 설정할 수 있습니다. TVSDK는 사용자가 검색할 때마다 이러한 범위(원하는 검색 위치가 `nonseekableRange` 내에 있는지 여부)를 확인합니다. 이 설정되고 사용자가 볼 수 없는 범위를 탐색하는 경우 TVSDK는 뷰어를 `seekableRange`의 종료 시간으로 강제 설정합니다.

* **START HERE** **** NEXTDefaultMetadataKeystrue 또는 false로 설정하여 라이브 스트림에서 프리롤 `ENABLE_LIVE_PREROLL` 을 활성화하거나 비활성화합니다. false인 경우 TVSDK는 컨텐츠 재생 전에 프리롤 광고에 대해 명시적 광고 서버 호출을 수행하지 않으므로 프리롤은 재생되지 않습니다. 이것은 중간 롤에 영향을 주지 않습니다. 기본값은 true입니다.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 이벤트 하위 유형 - TVSDK가 백그라운드 매니페스트에서 구독 태그를 감지할 때 전달됩니다.

* **알림**

   * `BACKGROUND_MANIFEST_WARNING`

      * 코드:204000
      * 유형:경고
      * 백그라운드 매니페스트 다운로드에 오류가 있습니다.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 검색할 수 없는 범위에서 검색을 시도하면 전달됩니다.


