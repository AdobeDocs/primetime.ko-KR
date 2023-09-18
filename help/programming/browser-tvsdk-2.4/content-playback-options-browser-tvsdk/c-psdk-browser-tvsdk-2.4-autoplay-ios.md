---
title: iOS에서 자동 재생
description: iOS에서 자동 재생
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# iOS에서 자동 재생{#autoplay-on-ios}

AdobePSDK.MediaPlayer의 볼륨 API를 구현하면 iOS 버전 10 이상을 실행하는 장치에서 컨텐츠를 자동으로 재생할 수 있습니다. iOS에서는 볼륨이 음소거된 경우에만 자동 재생을 허용합니다. 볼륨이 0으로 설정되면 API에서 `muted` 에 대한 비디오 태그의 속성 `true`, 그렇지 않으면 `muted` 속성이 로 설정되어 있습니다. `false`. 다음 `play` API는 사용자 상호 작용이나 사용자 제스처 없이 재생을 시작합니다.

iPhone에서 자동 재생의 경우 `playsInline` 의 속성 `video` 태그 위치: `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>사용 `playsInline` 속성은 전체 화면 모드 없이 재생을 시작합니다.
