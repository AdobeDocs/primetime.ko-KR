---
description: TVSDK는 라이브 비디오 스트림에서 일시 중단을 처리하고 일시 중단 중에 대체 콘텐츠를 제공합니다.
title: 일시 중단 처리
exl-id: 4a2ff371-69a9-4c13-ac61-3c5cd9c83a6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 일시 중단 처리 {#handle-blackouts}

TVSDK는 라이브 비디오 스트림에서 일시 중단을 처리하고 일시 중단 중에 대체 콘텐츠를 제공합니다.

프로그래밍 일시 중단과 관련된 가장 일반적인 사용 사례는 플레이어 앱이 기본 스트림을 시청할 수 없는 사용자에게 대체 콘텐츠를 제공하는 경우입니다. 이 앱은 TVSDK를 사용하여 일시 중단 기간의 시작과 끝을 확인할 수 있습니다. 이 방법으로 일시 중단 기간이 시작될 때 재생이 기본 스트림에서 대체 스트림으로 전환한 다음 일시 중단 기간이 끝나면 다시 기본 스트림으로 전환할 수 있습니다.

이 사용 사례에 대한 솔루션을 구현하려면 다음 작업을 수행하십시오.

1. 앱을 설정하여 라이브 스트림 매니페스트의 일시 중단 태그에 가입합니다.

   TVSDK는 일시 중단 태그를 직접 인식하지 않지만 매니페스트 파일 구문 분석 중에 특정 태그가 발생할 경우 앱에서 알림을 구독할 수 있습니다.
1. 에 대한 알림 수신기 추가 `PTTimedMetadataChangedNotification`.

   이 알림은 구독한 태그가 매니페스트에서 구문 분석될 때마다 발송되며 `PTTimedMetadata` 준비되었습니다.

1. 다음과 같은 리스너 메소드 구현 `onMediaPlayerSubscribedTagIdentified`, `PTTimedMetadata` 전경에 있는 개체입니다.

1. 재생 중에 업데이트가 있을 때마다 `PTMediaPlayerTimeChangeNotification` 처리할 리스너 `PTTimedMetadata` 개체.

1. 추가 `PTTimedMetadata` 핸들러입니다.

   이 핸들러를 사용하면 대체 콘텐츠로 전환하고 `PTTimedMetadata` 개체 및 해당 재생 시간입니다.

1. 사용 `onSubscribedTagInBackground` 리스너 메소드를 구현하려면 `PTTimedMetadata` 배경에 있는 개체입니다.

   이 메서드는 백그라운드 스트림의 타이밍을 모니터링하여 대체 콘텐츠에서 다시 주 콘텐츠로 전환할 수 있는 시기를 결정하는 데 도움이 됩니다.

1. 백그라운드 오류에 대해 수신기 메서드를 구현합니다.
1. 일시 중단 범위가 재생 스트림의 DVR에 있는 경우 찾을 수 없는 범위를 업데이트합니다.

   다음과 같은 경우 응용 프로그램에서 DVR에서 찾을 수 없는 범위를 설정해야 합니다.

   * DVR에서 일시 중단이 발생한 경우 기본 스트림에 연결할 때.
   * 대체 컨텐츠에서 기본 컨텐츠로 다시 전환할 때
