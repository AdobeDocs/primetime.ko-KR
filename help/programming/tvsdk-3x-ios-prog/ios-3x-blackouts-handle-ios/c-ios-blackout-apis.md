---
description: TVSDK는 메서드, 메타데이터 및 알림을 포함하여 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.
seo-description: TVSDK는 메서드, 메타데이터 및 알림을 포함하여 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.
seo-title: 일시 중단 API 요소
title: 일시 중단 API 요소
uuid: f87f4ed0-3f97-48bd-bceb-28357a978964
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# 일시 중단 API 요소 {#blackout-api-elements}

TVSDK는 메서드, 메타데이터 및 알림을 포함하여 일시 중단을 구현할 때 유용한 API 요소를 제공합니다.

플레이어에서 일시 중단 솔루션을 구현할 때 다음을 사용할 수 있습니다.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 현재 로드된 리소스를 배경 리소스로 저장합니다. 이 메서드 후에 `replaceCurrentItemWithPlayerItem`이(가) 호출되면 TVSDK는 `unregisterCurrentBackgroundItem`, `stop` 또는 `reset`을(를) 호출할 때까지 백그라운드 항목의 매니페스트를 계속 다운로드합니다.

   * `unregisterCurrentBackgroundItem` 배경 항목을 nil로 설정하고 배경 매니페스트를 가져오고 파싱하지 않습니다.

* **PTMetadata.** PTBlakoutMetadata `PTMetadata` 일시 중단에만 적용되는 클래스입니다.

   이를 통해 TVSDK에서 볼 수 없는 범위(`CMTimeRanges` 배열)를 설정할 수 있습니다. TVSDK는 사용자가 찾을 때마다 이러한 범위를 확인합니다. 이 설정이 되어 있고 사용자가 볼 수 없는 범위를 찾고자 할 경우 TVSDK는 뷰어를 볼 수 없는 범위의 끝으로 유도합니다.

* **START HERE** **** NEXTPTAdMetadataYES 또는 NO로 설정하여 라이브 스트림의 프리롤 `enableLivePreroll` 을 활성화하거나 비활성화합니다. NO인 경우 TVSDK는 컨텐츠 재생 전에 프리롤 광고에 대해 명시적인 광고 서버 호출을 수행하지 않으므로 프리롤은 재생되지 않습니다. 이것은 중간 롤에 영향을 주지 않습니다. 기본값은 YES입니다.

* **NSNotifications**

   * `PTTimedMetadataChangedInBackgroundNotification` - TVSDK에서 배경 매니페스트에서 구독 태그를 감지하면 게시되며 새  `PTTimedMetadata` 인스턴스가 배경에서 준비됩니다. 알림의 개체는 현재 재생 중인 `PTMediaPlayerItem` 인스턴스입니다. `PTTimedMetadataKey` 키를 사용하여 알림의 `userInfo` 사전에서 `PTTimedMetadata` 인스턴스를 가져올 수 있습니다.

   * `PTBackgroundManifestErrorNotification` - 미디어 플레이어에서 백그라운드 매니페스트를 완전히 로드하지 못할 때 게시됩니다. 즉, 모든 스트림 URL이 오류 또는 잘못된 응답을 반환합니다. 알림의 개체는 현재 재생 중인 `PTMediaPlayerItem` 인스턴스입니다.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * 코드:204000
      * 유형:경고
      * 백그라운드 매니페스트 다운로드에 오류가 있습니다.
   * `INVALID_SEEK_WARNING` 검색이 불가능한 범위( `nonSeekableRanges` 설정됨)에서 시도될 때  `PTBlackoutMetadata`전달됩니다.