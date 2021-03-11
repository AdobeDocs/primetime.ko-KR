---
description: 광고 동작을 사용자 정의하거나 재정의할 수 있습니다.
title: 사용자 정의 재생 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 사용자 정의된 재생 {#cset-up-customized-playback} 설정

광고 정책 인스턴스를 TVSDK에 등록하여 광고 동작을 사용자 정의하거나 재정의할 수 있습니다.

광고 동작을 사용자 정의하려면 다음 중 하나를 수행합니다.

* `AdPolicySelector` 인터페이스와 모든 메서드를 구현합니다.
모든 기본 광고 동작을 무시해야 하는 경우 이 옵션을 사용하는 것이 좋습니다.

* `DefaultAdPolicySelector` 클래스를 확장하고 필요한 비헤이비어에 대해서만 구현을 제공합니다.
사용자 지정.
이 옵션은 일부 기본 비헤이비어만 재정의해야 하는 경우에 좋습니다.

두 옵션 모두에 대해 다음 작업을 완료하십시오.

광고 비헤이비어를 사용자 정의하려면

1. AdPolicySelector 인터페이스와 모든 메서드를 구현합니다.

1. 광고 공장을 통해 TVSDK에서 사용할 정책 인스턴스를 지정합니다.

>[!IMPORTANT]
>
>>재생 시작 부분에 등록된 사용자 정의 광고 정책은 MediaPlayer 인스턴스가 >할당 해제 시 지워집니다. 응용 프로그램은 새 재생 세션이 생성될 때마다 정책 >선택기 인스턴스를 등록해야 합니다.

예:

```
    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. 사용자 정의 구현