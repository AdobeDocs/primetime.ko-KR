---
description: 브라우저 TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 만드는 도구를 제공합니다.
title: Flash 페일오버
exl-id: 76bd9214-767a-4f26-977d-81fbac3e0c42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Flash 페일오버 {#flash-failover}

브라우저 TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 만드는 도구를 제공합니다.

플랫폼의 도구를 사용하여 플레이어를 만들고, 비디오를 재생하고 관리하는 메서드가 있는 브라우저 TVSDK의 미디어 플레이어 보기에 연결합니다. 예를 들어 브라우저 TVSDK는 재생 및 일시 중지 메서드를 제공합니다. 플랫폼에서 사용자 인터페이스 단추를 만들고 해당 브라우저 TVSDK 메서드를 호출하도록 단추를 설정할 수 있습니다.

## Flash 대체 {#section_92D3884A13A6431F9A9CC5C79715D888}

브라우저 TVSDK에서 애플리케이션은 와 상호 작용합니다. `Primetime.js` API. 기본 브라우저 TVSDK 구현은 현재 플랫폼과 재생할 미디어의 리소스 유형을 기반으로 사용할 플레이어 기술을 결정합니다.

플레이어 기술에 대한 결정은 사용자가 호출할 때까지 수행되지 않습니다. `MediaPlayer.replaceCurrentResource` 특정 리소스를 재생합니다.

예:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## 사용할 미디어 플레이어 결정 {#section_D844E386AF5848688D204DEE258ECEE6}

이 샘플 절차는 플레이어 기술을 결정하는 프로세스를 보여 줍니다.

>[!TIP]
>
>프로세스는 URL 및 환경에 따라 달라질 수 있습니다.

1. Media Source Extensions가 지원되는 경우 알려진 제한 없이 사용하십시오.
1. 지원되는 경우 `<video>` MSE 없이 직접 태그 지정
1. Adobe Flash Player 버전 23.0 이상을 사용 중인지 확인하십시오.
1. 적절한 재생 기술을 찾지 못한 경우 `replaceCurrentResource` 오류를 반환합니다.

이후 `replaceCurrentResource` 동시에 호출 `MediaPlayer` 인스턴스는 동일한 프로세스를 따릅니다. 이를 통해 다양한 리소스 유형을 사용하여 재생할 수 있습니다 `MediaPlayer` 동일한 상위의 인스턴스 `<DIV>` 태그를에서 삭제할 때 지정한 `MediaPlayerView` 인스턴스가 생성되었습니다.

>[!TIP]
>
>SWF 개체 및 `<video>` 태그는 상위에 중첩됩니다. `<DIV>` 태그에 가깝게 배치하십시오.
