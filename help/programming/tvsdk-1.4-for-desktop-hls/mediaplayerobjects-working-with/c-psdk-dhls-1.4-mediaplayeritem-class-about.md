---
description: MediaPlayer 객체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어에서 오디오 또는 비디오를 나타냅니다.
title: MediaPlayerItem 클래스 정보
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# MediaPlayerItem 클래스 {#about-the-mediaplayeritem-class} 정보

MediaPlayer 객체는 미디어 플레이어를 나타냅니다. MediaPlayerItem은 플레이어에서 오디오 또는 비디오를 나타냅니다.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

미디어 리소스가 성공적으로 로드되면 TVSDK는 해당 리소스에 대한 액세스를 제공하기 위해 `MediaPlayerItem` 클래스의 인스턴스를 만듭니다.

`MediaResource`은 응용 프로그램 레이어가 컨텐트를 로드하기 위해 `MediaPlayer` 인스턴스로 실행하는 요청을 나타냅니다.

`MediaPlayer`은 미디어 리소스를 확인하고 연관된 매니페스트 파일을 로드한 다음 매니페스트를 파싱합니다. 리소스 로드 프로세스의 비동기 부분입니다. `MediaPlayerItem` 인스턴스는 리소스가 해결된 후 생성되며 이 인스턴스는 `MediaResource`의 해결된 버전입니다. TVSDK는 새로 만든 `MediaPlayerItem` 인스턴스에 대한 액세스 권한을 `MediaPlayer.currentItem`에 제공합니다.

>[!TIP]
>
>미디어 플레이어 항목에 액세스하려면 리소스가 성공적으로 로드될 때까지 기다려야 합니다.

