---
description: MediaResource는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-description: MediaResource는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-title: MediaPlayer 및 MediaResource 클래스
title: MediaPlayer 및 MediaResource 클래스
uuid: e198f599-22ca-4ea4-bbbb-e239c79174ae
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# MediaPlayer 및 MediaResource 클래스 {#mediaplayer-and-mediaresource-classes}

MediaResource는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK는 `MediaPlayer`의 `replaceCurrentResource` 메서드를 사용하여 재생 컨텐츠를 로드하고 준비하는 방법을 제공합니다. 이 메서드에는 두 개의 인수, 즉 `MediaPlayerResource`의 인스턴스와 선택적으로 응용 프로그램이 정의한 사용자 지정 매개 변수를 전달하는 데 사용할 수 있는 `MediaPlayerItemConfig`의 인스턴스가 사용됩니다.

* 자세한 내용은 [MediaPlayer 인스턴스 재사용 또는 제거](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayerobjects-working-with/android-3x-mediaplayer-reuse-or-remove.md)를 참조하십시오.
* `MediaPlayerResource`에 대한 자세한 내용은 [미디어 리소스 만들기](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-create.md)를 참조하십시오.