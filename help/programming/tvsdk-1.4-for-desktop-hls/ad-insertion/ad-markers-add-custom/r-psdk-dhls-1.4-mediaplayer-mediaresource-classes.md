---
description: MediaResource는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.
title: MediaPlayer 및 MediaResource 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# MediaPlayer 및 MediaResource 클래스{#mediaplayer-and-mediaresource-classes}

MediaResource는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK 라이브러리는 `MediaPlayer` 인터페이스에서 `replaceCurrentResource` 메서드를 사용하여 재생 콘텐츠를 간단히 로드하고 준비하는 방법을 제공합니다. 이 메서드는 단독 입력 인수로 `MediaResource` 클래스의 인스턴스를 받습니다. `MediaResource` 클래스는 다음 정보로 구성됩니다.

* 로드할 컨텐츠의 위치를 나타내는 URL입니다.
* 로드할 컨텐츠의 유형인 유형입니다.

   이 문자열은 `MediaPlayer`에서 로드할 수 있는 내용 유형을 정의하는 문자열입니다. 가능한 값은 HLS 및 HDS입니다. 각 값은 일반적으로 사용되는 파일 확장자를 나타내는 문자열(HLS의 경우 &quot;m3u8&quot;, HDS의 경우 &quot;f4m&quot;)과 연결됩니다.
* 일부 메타데이터 - `Metadata` 클래스의 인스턴스입니다.

   이 사전과 같은 구조에는 기본 컨텐츠에 배치해야 하는 대체/광고 컨텐츠에 대한 정보 등 로드하려는 컨텐츠에 대한 추가 정보가 포함될 수 있습니다.

메타데이터는 대체 컨텐츠와 관련된 정보가 TVSDK로 전달되는 매개변수입니다. `Metadata` 인터페이스는 키와 값이 모두 일반 문자열인 일반 키-값 저장소의 API를 정의합니다.
