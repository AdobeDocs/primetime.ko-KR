---
description: 'null'
seo-description: 'null'
seo-title: iOS 자동 재생
title: iOS 자동 재생
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# iOS 자동 재생{#autoplay-on-ios}

AdobePSDK.MediaPlayer의 볼륨 API를 구현하면 iOS 버전 10 이상을 실행하는 장치에서 컨텐츠를 자동 재생할 수 있습니다. iOS는 볼륨이 음소거된 경우에만 자동 재생을 허용합니다. 볼륨이 0으로 설정되면 API는 비디오 태그의 `muted` 속성을 `true`로 설정하고, 그렇지 않으면 `muted` 속성이 `false`로 설정됩니다. API는 `play` 사용자 상호 작용 또는 사용자 제스처 없이 재생을 시작합니다.

iPhone의 자동 재생의 경우 `playsInline` 태그의 `video` 속성을 로 설정합니다 `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>속성을 사용하면 전체 화면 모드 없이 재생을 시작할 수 `playsInline` 있습니다.

