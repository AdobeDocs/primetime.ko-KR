---
description: TVSDK 파섹
seo-description: TVSDK 파섹
seo-title: 일시 중단 API 요소
title: 일시 중단 API 요소
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 일시 중단 API 요소{#blackout-api-elements}

TVSDK 파섹

플레이어에서 일시 중단 솔루션을 구현할 때 다음을 사용할 수 있습니다.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 현재 로드된 리소스를 백그라운드 리소스로 저장합니다. 이 메서드 후에 `replaceCurrentResource` 호출되면 TVSDK는 사용자가 호출할 때까지 백그라운드 항목의 매니페스트를 계속 다운로드합니다 `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  현재 설정된 백그라운드 리소스를 삭제하고 배경 매니페스트의 가져오기 및 구문 분석을 중지합니다.

* **일시 중단메타데이터** 일시 중단과 관련된 메타데이터 유형입니다.

   이렇게 하면 TVSDK에서 볼 수 없는 범위(추가 `TimeRange` 속성이라고 함)를 설정할 `nonseekableRange`수 있습니다. TVSDK는 사용자가 검색할 때마다 이러한 범위(원하는 검색 위치가 a에 속하는지 `nonseekableRange`여부)를 확인합니다. 이 설정이 설정되어 사용자가 볼 수 없는 범위로 이동하면 TVSDK가 뷰어를 최종 `seekableRange`시간으로 전환합니다.

* **여기에서 시작 다음****DefaultMetadataKeys** `ENABLE_LIVE_PREROLL` true 또는 false로 설정하여 라이브 스트림에서 프리롤을 활성화하거나 비활성화합니다. false인 경우 TVSDK가 컨텐츠 재생 전에 프리롤 광고에 대해 명시적인 광고 서버 호출을 수행하지 않으므로 프리롤은 재생되지 않습니다. 이것은 중간 롤에 영향을 주지 않습니다. 기본값은 true입니다.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 이벤트 하위 유형 - TVSDK가 백그라운드 매니페스트에서 구독 태그를 감지할 때 전달됩니다.

* **알림**

   * `BACKGROUND_MANIFEST_WARNING`

      * 코드:204000년
      * 유형:경고
      * 백그라운드 매니페스트 다운로드에 오류가 있습니다.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` 검색할 수 없는 범위에서 검색을 시도하면 전달됩니다.


