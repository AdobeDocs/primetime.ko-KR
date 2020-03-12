---
description: MediaResource는 MediaPlayer 인스턴스가 로드하려고 하는 컨텐츠를 나타냅니다.
seo-description: MediaResource는 MediaPlayer 인스턴스가 로드하려고 하는 컨텐츠를 나타냅니다.
seo-title: MediaPlayer 및 MediaResource 클래스
title: MediaPlayer 및 MediaResource 클래스
uuid: e198f599-22ca-4ea4-bbbb-e239c79174ae
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# MediaPlayer 및 MediaResource 클래스 {#mediaplayer-and-mediaresource-classes}

MediaResource는 MediaPlayer 인스턴스가 로드하려고 하는 컨텐츠를 나타냅니다.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK는 에서 `replaceCurrentResource` 메서드를 사용하여 재생할 컨텐츠를 로드하고 준비하는 방법을 제공합니다 `MediaPlayer`. 이 메서드에는 응용 프로그램 정의 사용자 정의 매개 변수를 전달하는 데 사용할 수 있는 인스턴스 `MediaPlayerResource` 및 선택적으로 `MediaPlayerItemConfig`의 인스턴스와 같은 두 개의 인수가 필요합니다.

* 자세한 내용은 MediaPlayer [인스턴스](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayerobjects-working-with/android-3x-mediaplayer-reuse-or-remove.md)재사용 또는 제거를 참조하십시오.
* 자세한 `MediaPlayerResource`내용은 미디어 [리소스](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-create.md)만들기를 참조하십시오.