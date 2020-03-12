---
description: 광고 행동을 사용자 정의하거나 무시할 수 있습니다.
seo-description: 광고 행동을 사용자 정의하거나 무시할 수 있습니다.
seo-title: 사용자 정의 재생 설정
title: 사용자 정의 재생 설정
uuid: 9cbf0bcf-7932-409e-a690-e79f284eaf74
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 정의 가능한 재생 설정 {#cset-up-customized-playback}

TVSDK를 사용하여 광고 정책 인스턴스를 등록하여 광고 동작을 사용자 지정하거나 재정의할 수 있습니다.

광고 동작을 사용자 정의하려면 다음 중 하나를 수행합니다.

* 인터페이스와 모든 해당 메서드를 구현합니다. `AdPolicySelector` 
모든 기본 광고 동작을 무시해야 하는 경우 이 옵션을 사용하는 것이 좋습니다.

* 클래스를 `DefaultAdPolicySelector` 확장하고 사용자 지정이 필요한 비헤이비어에 대해서만 구현을 제공합니다.
이 옵션은 일부 기본 동작만 재정의해야 하는 경우에 권장됩니다.

두 옵션 모두에 대해 다음 작업을 완료하십시오.

광고 비헤이비어를 사용자 정의하려면

1. AdPolicySelector 인터페이스와 모든 메서드를 구현합니다.

1. 광고 공장을 통해 TVSDK에서 사용할 정책 인스턴스를 지정합니다.

>[!ATTENTION]
>
>>재생 시작 시 등록된 사용자 정의 광고 정책은 MediaPlayer 인스턴스가 >할당 취소될 때 지워집니다. 응용 프로그램은 새 재생 세션이 생성될 때마다 정책 >선택기 인스턴스를 등록해야 합니다.

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