---
description: MediaResource는 MediaPlayer 인스턴스가 로드하려고 하는 컨텐츠를 나타냅니다.
seo-description: MediaResource는 MediaPlayer 인스턴스가 로드하려고 하는 컨텐츠를 나타냅니다.
seo-title: MediaPlayer 및 MediaResource 클래스
title: MediaPlayer 및 MediaResource 클래스
uuid: 7393c320-7dbb-4580-9425-a735f9d03ef5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer 및 MediaResource 클래스{#mediaplayer-and-mediaresource-classes}

MediaResource는 MediaPlayer 인스턴스가 로드하려고 하는 컨텐츠를 나타냅니다.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK 라이브러리는 MediaPlayer 인터페이스의 메서드를 사용하여 컨텐츠를 로드하고 재생할 수 있는 간단한 방법을 `replaceCurrentItem` 제공합니다. 이 메서드는 MediaResource 클래스의 인스턴스를 단독 입력 인수로 받습니다. MediaResource 클래스는 다음 정보로 구성됩니다.

* 로드할 컨텐츠의 위치를 나타내는 URL입니다.
* 로드할 컨텐츠의 유형인 유형입니다.

   MediaPlayer에서 로드할 수 있는 컨텐츠 유형을 정의하는 클래스의 단순 열거형입니다. `MediaResource` 가능한 값은 HLS 및 HDS입니다. 각 값은 HLS와 HDS의 경우 일반적으로 사용되는 파일 확장자를 나타내는 `m3u8` 문자열에 `f4m` 연결됩니다.
* 일부 메타데이터는 `Metadata` 클래스의 인스턴스입니다.

   사전 같은 구조에는 기본 컨텐츠에 배치해야 하는 대체/광고 컨텐츠와 같은 로드하려는 컨텐츠에 대한 추가 정보가 포함될 수 있습니다.

메타데이터는 대체 컨텐츠와 관련된 정보가 TVSDK로 전달되는 매개체입니다. 이 `Metadata` 인터페이스는 키와 값이 모두 일반 문자열인 일반 키 값 저장소에 대한 API를 정의합니다.
