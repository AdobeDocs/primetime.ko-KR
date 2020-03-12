---
description: Browser TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하는 데 필요한 툴을 제공합니다.
seo-description: Browser TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하는 데 필요한 툴을 제공합니다.
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 플래시 장애 조치 {#flash-failover}

Browser TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하는 데 필요한 툴을 제공합니다.

플랫폼의 툴을 사용하여 플레이어를 만들고 비디오를 재생하고 관리하는 방법을 제공하는 브라우저 TVSDK의 미디어 플레이어 보기에 연결할 수 있습니다. 예를 들어, 브라우저 TVSDK는 재생 및 일시 중지 메서드를 제공합니다. 플랫폼에서 사용자 인터페이스 단추를 만들고 해당 Browser TVSDK 메서드를 호출하도록 단추를 설정할 수 있습니다.

## Flash 폴백 {#section_92D3884A13A6431F9A9CC5C79715D888}

Browser TVSDK에서 응용 프로그램은 API와 상호 `Primetime.js` 작용합니다. 기본 브라우저 TVSDK 구현은 현재 플랫폼과 재생할 미디어의 리소스 유형을 기반으로 사용할 플레이어 기술을 결정합니다.

플레이어 기술에 대한 결정은 특정 리소스를 재생하도록 호출하기 전까지 `MediaPlayer.replaceCurrentResource` 수행되지 않습니다.

예:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## 사용할 미디어 플레이어 결정 {#section_D844E386AF5848688D204DEE258ECEE6}

이 샘플 절차에서는 플레이어 기술을 결정하는 과정을 보여 줍니다.

>[!TIP]
>
>프로세스는 URL 및 환경에 따라 달라질 수 있습니다.

1. 미디어 소스 확장이 지원되는 경우 알려진 제한 없이 사용하십시오.
1. 지원되는 경우 MSE 없이 바로 `<video>` 태그를 사용하십시오.
1. Adobe Flash Player 버전 23.0 이상을 사용하고 있는지 확인합니다.
1. 적절한 재생 기술이 없는 경우 `replaceCurrentResource` 오류를 반환합니다.

동일한 인스턴스에 대한 후속 `replaceCurrentResource` `MediaPlayer` 호출은 동일한 프로세스를 따릅니다. 이렇게 하면 인스턴스를 만들 때 지정한 동일한 상위 `MediaPlayer` 태그에서 동일한 `<DIV>` 인스턴스를 사용하여 다양한 리소스 유형을 재생할 수 `MediaPlayerView` 있습니다.

>[!TIP]
>
>SWF 객체와 `<video>` 태그는 상위 `<DIV>` 태그에 중첩됩니다.

