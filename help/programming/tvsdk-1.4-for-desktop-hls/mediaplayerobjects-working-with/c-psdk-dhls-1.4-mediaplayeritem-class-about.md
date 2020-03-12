---
description: MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어의 오디오 또는 비디오를 나타냅니다.
seo-description: MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어의 오디오 또는 비디오를 나타냅니다.
seo-title: MediaPlayerItem 클래스 정보
title: MediaPlayerItem 클래스 정보
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# MediaPlayerItem 클래스 정보{#about-the-mediaplayeritem-class}

MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어의 오디오 또는 비디오를 나타냅니다.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

미디어 리소스가 성공적으로 로드되면 TVSDK는 해당 리소스에 대한 액세스를 제공하기 위해 `MediaPlayerItem` 클래스의 인스턴스를 만듭니다.

응용 프로그램 `MediaResource` 레이어가 컨텐츠를 로드하기 위해 인스턴스에 실행하는 요청을 나타냅니다 `MediaPlayer` .

미디어 리소스를 `MediaPlayer` 확인하고 연결된 매니페스트 파일을 로드하며 매니페스트를 구문 분석합니다. 리소스 로드 프로세스의 비동기 부분입니다. 리소스가 해결된 후 `MediaPlayerItem` 인스턴스가 생성되며 이 인스턴스는 해결된 버전의 `MediaResource`입니다. TVSDK는 새로 생성된 `MediaPlayerItem` 인스턴스를 통해 액세스할 수 `MediaPlayer.currentItem`있습니다.

>[!TIP]
>
>미디어 플레이어 항목에 액세스하려면 리소스가 성공적으로 로드될 때까지 기다려야 합니다.

