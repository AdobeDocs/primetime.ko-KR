---
title: 비디오 재생의 필수 작업
description: PlaybackManager는 HLS 스트리밍의 필수 작업을 제공합니다.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 비디오 재생의 필수 작업 {#essential-operations-of-video-playback}

PlaybackManager는 HLS 스트리밍에 대한 필수 작업을 제공합니다.

* 비디오 이벤트에 적절하게 응답할 수 있는 [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)를 호출합니다.
* 재생, 일시 정지 및 찾기와 같은 재생 작업을 제공합니다.
* 플레이어 상태, 재생 범위 및 비디오 라이브 스트림과 같은 플레이어 정보를 반환합니다.
* ABR이 활성화되었는지 확인하고 제공된 구성 데이터에 따라 ABR 및 버퍼 컨트롤 매개 변수를 설정합니다.
* 버퍼 컨트롤이 활성화되었는지 확인하고 제공된 구성 데이터에 따라 버퍼 컨트롤 매개 변수를 설정합니다.