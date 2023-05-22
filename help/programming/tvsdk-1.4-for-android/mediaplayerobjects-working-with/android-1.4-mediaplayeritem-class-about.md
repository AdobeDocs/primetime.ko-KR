---
description: MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어의 오디오 또는 비디오를 나타냅니다.
title: MediaPlayerItem 클래스 정보
exl-id: 07105fab-0338-4410-93f3-e337d46d9de5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# MediaPlayerItem 클래스 정보{#about-the-mediaplayeritem-class}

MediaPlayer 개체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어의 오디오 또는 비디오를 나타냅니다.

미디어 리소스가 성공적으로 로드되면 TVSDK는 `MediaPlayerItem` 클래스에 대한 액세스 권한을 제공합니다.

다음 `MediaResource` 는 애플리케이션 계층에서 `MediaPlayer` 컨텐츠를 로드할 인스턴스입니다.

다음 `MediaPlayer` 미디어 리소스를 확인하고, 연결된 매니페스트 파일을 로드하고, 매니페스트를 구문 분석합니다. 리소스 로드 프로세스의 비동기적 부분입니다. 다음 `MediaPlayerItem` 리소스가 해결된 후 인스턴스가 생성되며 이 인스턴스는 의 해결된 버전입니다. `MediaResource`. TVSDK는 새로 만든 항목에 대한 액세스 권한을 제공합니다 `MediaPlayerItem` 인스턴스 - `MediaPlayer.CurrentItem`

>[!TIP]
>
>미디어 플레이어 항목에 액세스하기 전에 리소스가 성공적으로 로드될 때까지 기다려야 합니다.
