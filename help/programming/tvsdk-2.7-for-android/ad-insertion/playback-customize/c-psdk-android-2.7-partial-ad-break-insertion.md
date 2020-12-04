---
description: 'null'
seo-description: 'null'
seo-title: 부분 광고 분리 삽입
title: 부분 광고 분리 삽입
uuid: cc071c89-f813-419e-a2b2-4f6a9fdccd6a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 부분 광고 분리 삽입 {#partial-ad-break-insertion}

TV와 같은 경험을 통해 광고 중간에 라이브 스트림으로 참여할 수 있습니다. 부분 광고 중단 기능을 사용하면 클라이언트가 중간 롤에서 라이브 스트림을 시작하는 경우 해당 중간 롤에서 시작되는 TV와 같은 경험을 모방할 수 있습니다. TV채널로 전환해 TV를 방영하는 것과 비슷한 방식이다.

예를 들어 사용자가 90초 광고 중단(3개의 30초 광고)의 중간에 참여하는 경우, 두 번째 광고(즉, 광고 나누기로 40초 후)에 10초 동안 참여하는 경우, 다음이 발생합니다.

* 두 번째 광고는 나머지 기간(20초) 뒤에 세 번째 광고가 재생됩니다.
* 부분적으로 재생된 광고(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기만 실행됩니다.

이 동작은 기본적으로 활성화되어 있지 않습니다. 앱에서 이 기능을 사용하려면 다음을 수행하십시오.

1. AdvertisingMetadata 클래스의 메서드 setEnableLivePreroll을 사용하여 라이브 프리롤을 비활성화합니다.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. 부분 광고 삽입 환경 설정을 켜십시오. MediaPlayer 인터페이스의 새로운 메서드 setPartialAdBreakPref를 사용하여 이 기능을 ON으로 전환합니다. getPartialAdBreakPref 메서드를 사용하여 이 기본 설정의 현재 상태를 찾습니다.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```

