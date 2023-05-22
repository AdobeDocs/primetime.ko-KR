---
description: MediaResource가 성공적으로 로드되면 브라우저 TVSDK는 MediaPlayerItem 클래스의 인스턴스를 만들어 해당 리소스에 대한 액세스를 제공합니다.
title: MediaPlayerItem 클래스 정보
exl-id: 6e47914c-3d46-4aaf-9144-1a00d886e5bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# MediaPlayerItem 클래스 정보{#about-the-mediaplayeritem-class}

MediaResource가 성공적으로 로드되면 브라우저 TVSDK는 MediaPlayerItem 클래스의 인스턴스를 만들어 해당 리소스에 대한 액세스를 제공합니다.

다음 `MediaResource` 는 애플리케이션 계층에서 `MediaPlayer` 컨텐츠를 로드할 인스턴스입니다.

다음 `MediaPlayer` 미디어 리소스를 확인하고, 연결된 매니페스트 파일을 로드하고, 매니페스트를 구문 분석합니다. 리소스 로드 프로세스의 비동기적 부분입니다. 다음 `MediaPlayerItem` 리소스가 해결된 후 인스턴스가 생성되며 이 인스턴스는 의 해결된 버전입니다. `MediaResource`. 브라우저 TVSDK는 새로 만든 항목에 대한 액세스 권한을 제공합니다 `MediaPlayerItem` 인스턴스 - `MediaPlayer.CurrentItem`.

>[!TIP]
>
>미디어 플레이어 항목에 액세스하기 전에 리소스가 성공적으로 로드될 때까지 기다려야 합니다.
