---
description: MediaResource는 MediaPlayer 인스턴스에서 로드하려는 콘텐츠를 나타냅니다.
title: MediaPlayer 및 MediaResource 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# MediaPlayer 및 MediaResource 클래스{#mediaplayer-and-mediaresource-classes}

MediaResource는 MediaPlayer 인스턴스에서 로드하려는 콘텐츠를 나타냅니다.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK 라이브러리는 를 사용하여 재생할 콘텐츠를 로드하고 준비하는 간단한 방법을 제공합니다. `replaceCurrentResource` 의 메서드 `MediaPlayer` 인터페이스. 이 메서드는 의 인스턴스를 받습니다. `MediaResource` 클래스를 유일한 입력 인수로 사용합니다. 다음 `MediaResource` 클래스는 다음 정보로 구성됩니다.

* 로드하려는 콘텐츠의 위치를 나타내는 URL입니다.
* 유형: 곧 로드될 콘텐츠의 유형입니다.

  이 문자열은에서 로드할 수 있는 콘텐츠 유형을 정의합니다. `MediaPlayer`. 가능한 값은 HLS 및 HDS입니다. 각 값은 일반적으로 사용되는 파일 확장자를 나타내는 문자열(HLS의 경우 &quot;m3u8&quot;, HDS의 경우 &quot;f4m&quot;)과 연결됩니다.
* 의 인스턴스인 일부 메타데이터 `Metadata` 클래스.

  이 사전과 유사한 구조에는 기본 콘텐츠에 배치해야 하는 대체/광고 콘텐츠에 대한 정보와 같이 로드하려는 콘텐츠에 대한 추가 정보가 포함될 수 있습니다.

메타데이터는 대체 콘텐츠와 관련된 정보가 TVSDK에 전달되는 매체입니다. 다음 `Metadata` 인터페이스는 키와 값이 모두 일반 문자열인 일반 키-값 저장소에 대한 API를 정의합니다.
