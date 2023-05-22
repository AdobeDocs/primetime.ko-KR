---
description: TVSDK는 메서드, 메타데이터 및 알림을 포함하여 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.
title: 일시 중단 API 요소
exl-id: 76d99d8d-1aae-4faa-aaf2-bb7b535a1c71
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 일시 중단 API 요소 {#blackout-api-elements}

TVSDK는 메서드, 메타데이터 및 알림을 포함하여 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.

플레이어에서 일시 중단 솔루션을 구현할 때 다음 사항을 사용할 수 있습니다.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 현재 로드된 리소스를 백그라운드 리소스로 저장합니다. If `replaceCurrentItemWithPlayerItem` 이 메서드 다음에 가 호출되면 호출할 때까지 TVSDK에서 배경 항목의 매니페스트를 계속 다운로드합니다. `unregisterCurrentBackgroundItem` , `stop`, 또는 `reset` .

   * `unregisterCurrentBackgroundItem` 백그라운드 항목을 nil로 설정하고 백그라운드 매니페스트의 가져오기 및 구문 분석을 중지합니다.

* **PTMetadata.PTBlackoutMetadata** A `PTMetadata` 일시 중단에만 해당되는 클래스입니다.

   이렇게 하면 찾을 수 없는 범위(배열)를 설정할 수 있습니다. `CMTimeRanges`TVSDK의 ) TVSDK는 사용자가 검색할 때마다 이러한 범위를 확인합니다. 설정되어 있고 사용자가 검색할 수 없는 범위를 찾는 경우 TVSDK는 뷰어를 검색할 수 없는 범위의 끝으로 강제 적용합니다.

* **다음 위치에서 시작** **PTAdMetadata** 를 설정하여 라이브 스트림에서 프리롤 활성화 또는 비활성화 `enableLivePreroll` 예 또는 아니오로. NO인 경우, TVSDK는 컨텐츠 재생 전에 프리롤 광고에 대한 명시적 광고 서버 호출을 수행하지 않으므로 프리롤을 재생하지 않습니다. 중간 롤에는 영향을 주지 않습니다. 기본값은 YES입니다.

* **NSNotifications**

   * `PTTimedMetadataChangedInBackgroundNotification` - TVSDK가 백그라운드 매니페스트에서 구독 중인 태그 및 새 태그를 검색하면 게시됨 `PTTimedMetadata` 인스턴스는 이 인스턴스에서 준비됩니다. 알림의 개체는 입니다. `PTMediaPlayerItem` 현재 재생 중인 인스턴스. 다음을 가져올 수 있습니다. `PTTimedMetadata` 알림의 인스턴스 `userInfo` 사전을 사용하여 `PTTimedMetadataKey` 키.

   * `PTBackgroundManifestErrorNotification` - 미디어 플레이어가 배경 매니페스트를 완전히 로드하지 못할 때, 즉 모든 스트림 URL이 오류 또는 잘못된 응답을 반환하는 경우 게시됩니다. 알림의 개체는 입니다. `PTMediaPlayerItem` 현재 재생 중인 인스턴스.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 코드: 204000
      * 유형: 경고
      * 백그라운드 매니페스트 다운로드 중 오류가 발생했습니다.
   * `INVALID_SEEK_WARNING` 검색할 수 없는 범위(에서 찾기가 시도되면 발송 `nonSeekableRanges` 설정 `PTBlackoutMetadata`).
