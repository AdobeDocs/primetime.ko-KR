---
title: 부분 광고 브레이크 삽입
description: 부분 광고 브레이크 삽입
copied-description: true
exl-id: c86f1e99-7f1e-4a1e-b285-568ad6659f45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# 부분 광고 브레이크 삽입 {#partial-ad-break-insertion}

라이브 스트림에서 광고 중간에 참가할 수 있는 TV와 유사한 경험을 활성화할 수 있습니다. 부분 광고 브레이크 기능을 사용하면 클라이언트가 미드롤 내에서 라이브 스트림을 시작하는 경우 해당 미드롤 내에서 시작되는 TV와 유사한 경험을 모방할 수 있습니다. TV로 갈아타는 것과 비슷하고 광고도 쉴 새 없이 흘러간다.

예를 들어 사용자가 90초 광고 브레이크(3개의 30초 광고)의 중간에서 두 번째 광고에 10초 동안(즉, 광고 브레이크에 40초 동안) 가입하면 다음과 같은 일이 발생합니다.

* 두 번째 광고는 나머지 기간(20초) 동안 재생되고 그 뒤에는 세 번째 광고가 재생됩니다.
* 부분적으로 재생된 광고(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기만 실행됩니다.

이 동작은 기본적으로 활성화되어 있지 않습니다. 앱에서 이 기능 작업을 활성화하려면 다음을 수행하십시오.

부분 광고 브레이크 삽입 환경 설정을 켭니다. 새 메서드 사용 `setPartialAdBreakPref` 이 기능을 켜도록 MediaPlayer 인터페이스에서 설정합니다. 사용 `getPartialAdBreakPref` 메서드를 사용하여 이 환경 설정의 현재 상태를 찾을 수 있습니다.

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

프리롤 광고(사용 가능한 경우)가 재생되면 라이브 TV 환경을 에뮬레이션하여 라이브 포인트에서 콘텐츠가 재생됩니다.
