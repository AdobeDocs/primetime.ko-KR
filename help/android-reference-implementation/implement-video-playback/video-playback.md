---
seo-title: 비디오 재생에 필수적인 작업
title: 비디오 재생에 필수적인 작업
description: PlaybackManager는 HLS 스트리밍의 필수 작업을 제공합니다.
seo-description: PlaybackManager는 HLS 스트리밍의 필수 작업을 제공합니다.
uuid: 7ac93f1f-9233-4462-a4be-528d1aa524a9
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 비디오 재생에 필수적인 작업 {#essential-operations-of-video-playback}

PlaybackManager는 HLS 스트리밍에 대한 필수 작업을 제공합니다.

* 비디오 이벤트에 [적절하게 응답할 수 있는](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)PlaybackManagerEventListener를 호출합니다.
* 재생, 일시 중지 및 찾기와 같은 재생 작업을 제공합니다.
* 플레이어 상태, 재생 범위 및 비디오 라이브 스트림과 같은 플레이어 정보를 반환합니다.
* ABR이 활성화되었는지 확인하고 제공된 구성 데이터에 따라 ABR 및 버퍼 컨트롤 매개 변수를 설정합니다.
* 버퍼 컨트롤이 활성화되었는지 확인하고 제공된 구성 데이터에 따라 버퍼 컨트롤 매개 변수를 설정합니다.