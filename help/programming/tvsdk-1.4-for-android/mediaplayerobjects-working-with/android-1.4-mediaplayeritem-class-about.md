---
description: MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어에서 오디오 또는 비디오를 나타냅니다.
seo-description: MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어에서 오디오 또는 비디오를 나타냅니다.
seo-title: MediaPlayerItem 클래스 정보
title: MediaPlayerItem 클래스 정보
uuid: d7f65edf-4693-4b1e-bae0-46fadce98751
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# MediaPlayerItem 클래스 정보{#about-the-mediaplayeritem-class}

MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어에서 오디오 또는 비디오를 나타냅니다.

미디어 리소스가 성공적으로 로드되면 TVSDK는 해당 리소스에 대한 액세스를 제공하기 위해 `MediaPlayerItem` 클래스의 인스턴스를 만듭니다.

`MediaResource`은 응용 프로그램 레이어가 컨텐트를 로드할 `MediaPlayer` 인스턴스에 의해 실행된 요청을 나타냅니다.

`MediaPlayer`은 미디어 리소스를 확인하고, 연관된 매니페스트 파일을 로드하고 매니페스트를 구문 분석합니다. 리소스 로드 프로세스의 비동기 부분입니다. `MediaPlayerItem` 인스턴스는 리소스가 해결된 후 생성되며 이 인스턴스는 `MediaResource`의 해결된 버전입니다. TVSDK는 새로 만든 `MediaPlayerItem` 인스턴스에 대한 액세스 권한을 `MediaPlayer.CurrentItem` 통해 제공합니다

>[!TIP]
>
>미디어 플레이어 항목에 액세스하기 전에 리소스가 성공적으로 로드될 때까지 기다려야 합니다.

