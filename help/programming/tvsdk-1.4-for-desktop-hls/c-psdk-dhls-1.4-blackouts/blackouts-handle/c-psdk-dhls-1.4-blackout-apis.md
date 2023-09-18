---
description: TVSDK는 메서드, 메타데이터 및 알림을 포함하여 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.
title: 일시 중단 API 요소
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 일시 중단 API 요소{#blackout-api-elements}

TVSDK는 메서드, 메타데이터 및 알림을 포함하여 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.

플레이어에서 일시 중단 솔루션을 구현할 때 다음 사항을 사용할 수 있습니다.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 현재 로드된 리소스를 백그라운드 리소스로 저장합니다. If `replaceCurrentResource` 이 메서드 다음에 가 호출되면 호출할 때까지 TVSDK에서 배경 항목의 매니페스트를 계속 다운로드합니다. `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  현재 설정된 백그라운드 리소스를 지우고 백그라운드 매니페스트의 가져오기 및 구문 분석을 중지합니다.

* **일시 중단 메타데이터** 일시 중단과 관련된 메타데이터 유형입니다.

  이렇게 하면 찾을 수 없는 범위를 설정할 수 있습니다(추가 기능 제공) `TimeRange` 속성 호출됨 `nonseekableRange`TVSDK의 ) TVSDK는 이러한 범위(원하는 검색 위치가 다음 내에 속하는지 여부)를 확인합니다. `nonseekableRange`) 사용자가 찾을 때마다. 설정된 경우 사용자가 검색할 수 없는 범위를 찾는 경우 TVSDK는 뷰어를 의 종료 시간으로 강제 적용합니다. `seekableRange`.

* **다음 위치에서 시작** **기본 메타데이터 키** 를 설정하여 라이브 스트림에서 프리롤 활성화 또는 비활성화 `ENABLE_LIVE_PREROLL` true 또는 false입니다. false인 경우 TVSDK는 컨텐츠 재생 전에 프리롤 광고에 대한 명시적 광고 서버 호출을 수행하지 않으므로 프리롤을 재생하지 않습니다. 중간 롤에는 영향을 주지 않습니다. 기본값은 true입니다.

* **TimedMetaEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` 이벤트 하위 유형 - TVSDK가 백그라운드 매니페스트에서 구독한 태그를 검색하면 발송됩니다.

* **알림**

   * `BACKGROUND_MANIFEST_WARNING`

      * 코드: 204000
      * 유형: 경고
      * 백그라운드 매니페스트 다운로드 중 오류가 발생했습니다.

   * `SeekEvent.SEEK_POSITION_ADJUSTED` 검색할 수 없는 범위에서 찾기가 시도되면 발송됩니다.
