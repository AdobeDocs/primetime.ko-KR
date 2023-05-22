---
title: 비디오 재생의 필수 작업
description: PlaybackManager는 HLS 스트리밍의 필수 작업을 제공합니다
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 비디오 재생의 필수 작업 {#essential-operations-of-video-playback}

PlaybackManager는 HLS 스트리밍의 필수 작업을 제공합니다.

* 호출 [PlaybackManagerEventListen](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html): 비디오 이벤트에 적절하게 응답할 수 있습니다.
* 재생, 일시 중지, 찾기 등 재생 작업을 제공합니다.
* 플레이어 상태, 재생 범위 및 비디오 라이브 스트림과 같은 플레이어에 대한 정보를 반환합니다.
* ABR의 활성화 여부를 확인하고 제공된 구성 데이터에 따라 ABR 및 버퍼 제어 매개 변수를 설정합니다.
* 버퍼 제어의 사용 여부를 결정하고 제공된 구성 데이터에 따라 버퍼 제어 매개 변수를 설정합니다.
