---
description: TVSDK는 광고 세그먼트를 다운로드하고 장치의 화면에 표시합니다.
seo-description: TVSDK는 광고 세그먼트를 다운로드하고 장치의 화면에 표시합니다.
seo-title: 광고 재생 단계
title: 광고 재생 단계
uuid: 1bbcea08-3475-4a64-9f89-c455d5dd828e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# 광고 재생 단계{#ad-playback-phase}

TVSDK는 광고 세그먼트를 다운로드하고 장치의 화면에 표시합니다.

이때 TVSDK는 광고를 해결하고 타임라인에 광고를 배치하며 화면에 컨텐츠를 렌더링하려고 시도합니다.

이 단계에서는 다음과 같은 오류 기본 클래스가 발생할 수 있습니다.

* 호스트 서버에 연결할 때 오류 발생
* 매니페스트 파일을 다운로드하는 동안 오류가 발생했습니다.
* 미디어 세그먼트를 다운로드할 때 오류 발생

세 개의 오류 클래스에 대해 TVSDK는 트리거된 이벤트를 애플리케이션으로 전달합니다. 여기에는 다음이 포함됩니다.

* 장애 조치(failover)가 발생할 때 알림 이벤트가 트리거됩니다.
* 장애 조치(failover) 알고리즘 때문에 프로필이 변경될 때의 알림 이벤트.
* 모든 장애 조치 옵션이 고려되고 추가 작업을 자동으로 수행할 수 없을 때 알림 이벤트가 트리거됩니다.

   애플리케이션은 적절한 조치를 취해야 합니다.

오류 발생 여부와 관계없이 TVSDK는 모든 `onAdStart`에 대해 각각 `onAdBreakStart` 및 `onAdComplete`에 대해 onAdBreakComplete를 호출합니다. 하지만 세그먼트를 다운로드할 수 없는 경우 타임라인에 간격이 있을 수 있습니다. 간격이 충분히 커지면 재생 헤드 위치 및 보고된 광고 진행에 있는 값이 불연속적일 수 있습니다.
