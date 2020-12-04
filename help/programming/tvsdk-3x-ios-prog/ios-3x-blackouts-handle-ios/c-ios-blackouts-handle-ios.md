---
description: TVSDK는 실시간 비디오 스트림의 일시 중단을 처리하고 일시 중단 동안 대체 컨텐츠를 제공합니다.
seo-description: TVSDK는 실시간 비디오 스트림의 일시 중단을 처리하고 일시 중단 동안 대체 컨텐츠를 제공합니다.
seo-title: 일시 중단 처리
title: 일시 중단 처리
uuid: 00b6f204-6ba4-4245-9028-6f7c392e9275
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# 일시 중단 처리 {#handle-blackouts}

TVSDK는 실시간 비디오 스트림의 일시 중단을 처리하고 일시 중단 동안 대체 컨텐츠를 제공합니다.

프로그래밍 일시 중단과 관련된 가장 일반적인 사용 사례는 플레이어 앱에서 기본 스트림을 볼 수 없는 사용자에게 대체 컨텐츠를 제공하는 경우입니다. 이 앱은 TVSDK를 사용하여 일시 중단 기간의 시작과 끝을 결정할 수 있습니다. 이렇게 일시 중단 기간이 시작될 때 재생을 주 스트림에서 대체 스트림으로 전환한 다음 일시 중단 기간이 끝나면 주 스트림으로 다시 전환할 수 있습니다.

이 사용 사례에 대한 솔루션을 구현하려면

1. 라이브 스트림 매니페스트의 일시 중단 태그에 가입하도록 앱을 설정합니다.

   TVSDK는 일시 중단 태그를 직접 인식하지 못하지만 매니페스트 파일 구문 분석 동안 특정 태그가 발생하는 경우 앱에서 알림에 가입할 수 있습니다.
1. `PTTimedMetadataChangedNotification`에 대한 알림 수신기를 추가합니다.

   이 알림은 가입된 태그를 매니페스트에서 구문 분석할 때마다 전달되며, 이 알림에서 새 `PTTimedMetadata`이 준비됩니다.

1. 전경의 `PTTimedMetadata` 개체에 대해 `onMediaPlayerSubscribedTagIdentified` 등의 수신기 메서드를 구현합니다.

1. 재생 중에 업데이트가 있을 때마다 `PTMediaPlayerTimeChangeNotification` 리스너를 사용하여 `PTTimedMetadata` 개체를 처리합니다.

1. `PTTimedMetadata` 핸들러를 추가합니다.

   이 핸들러를 사용하면 대체 컨텐츠로 전환하여 `PTTimedMetadata` 개체 및 해당 재생 시간에 지정된 기본 컨텐츠로 돌아갈 수 있습니다.

1. 백그라운드에서 `PTTimedMetadata` 개체에 대한 수신기 메서드를 구현하려면 `onSubscribedTagInBackground`을 사용합니다.

   이 방법은 백그라운드 스트림의 타이밍을 모니터링하므로 대체 컨텐츠에서 기본 컨텐츠로 다시 전환할 수 있는 시기를 결정할 수 있습니다.

1. 배경 오류에 대한 리스너 메서드를 구현합니다.
1. 일시 중단 범위가 재생 스트림의 DVR에 있는 경우 검색할 수 없는 범위를 업데이트합니다.

   다음 경우 애플리케이션에서 DVR에서 볼 수 없는 범위를 설정해야 합니다.

   * 일시 중단이 DVR에 있을 때 기본 스트림에 연결할 때.
   * 대체 컨텐츠에서 기본 컨텐츠로 다시 전환할 때.