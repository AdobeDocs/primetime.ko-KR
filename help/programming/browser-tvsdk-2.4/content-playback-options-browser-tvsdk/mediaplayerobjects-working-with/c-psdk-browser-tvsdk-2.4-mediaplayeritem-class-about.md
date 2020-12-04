---
description: MediaResource가 성공적으로 로드되면 Browser TVSDK가 MediaPlayerItem 클래스의 인스턴스를 만들어 해당 리소스에 액세스할 수 있습니다.
seo-description: MediaResource가 성공적으로 로드되면 Browser TVSDK가 MediaPlayerItem 클래스의 인스턴스를 만들어 해당 리소스에 액세스할 수 있습니다.
seo-title: MediaPlayerItem 클래스 정보
title: MediaPlayerItem 클래스 정보
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# MediaPlayerItem 클래스 정보{#about-the-mediaplayeritem-class}

MediaResource가 성공적으로 로드되면 Browser TVSDK가 MediaPlayerItem 클래스의 인스턴스를 만들어 해당 리소스에 액세스할 수 있습니다.

`MediaResource`은 응용 프로그램 레이어가 컨텐트를 로드할 `MediaPlayer` 인스턴스에 의해 실행된 요청을 나타냅니다.

`MediaPlayer`은 미디어 리소스를 확인하고, 연관된 매니페스트 파일을 로드하고 매니페스트를 구문 분석합니다. 리소스 로드 프로세스의 비동기 부분입니다. `MediaPlayerItem` 인스턴스는 리소스가 해결된 후 생성되며 이 인스턴스는 `MediaResource`의 해결된 버전입니다. 브라우저 TVSDK는 새로 만든 `MediaPlayerItem` 인스턴스에 대한 액세스 권한을 `MediaPlayer.CurrentItem`에서 제공합니다.

>[!TIP]
>
>미디어 플레이어 항목에 액세스하기 전에 리소스가 성공적으로 로드될 때까지 기다려야 합니다.

