---
description: 광고 비헤이비어를 사용자 정의하거나 재정의할 수 있습니다.
title: 사용자 지정 재생 설정
exl-id: aaa4d1c2-c425-4a2e-8377-0a3072f3fb18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 사용자 지정 재생 설정 {#cset-up-customized-playback}

TVSDK에 광고 정책 인스턴스를 등록하여 광고 동작을 사용자 정의하거나 재정의할 수 있습니다.

광고 동작을 사용자 지정하려면 다음 중 하나를 수행하십시오.

* 구현 `AdPolicySelector` 인터페이스 및 모든 해당 메서드.
모든 기본 광고 동작을 재정의해야 하는 경우 이 옵션을 사용하는 것이 좋습니다.

* 확장 `DefaultAdPolicySelector` 클래스를 만들고 맞춤화가 필요한 비헤이비어에 대해서만 구현을 제공합니다.
기본 동작 중 일부만 재정의해야 하는 경우에는 이 옵션을 사용하는 것이 좋습니다.

두 옵션 모두 다음 작업을 완료하십시오.

광고 비헤이비어를 사용자 지정하려면:

1. AdPolicySelector 인터페이스 및 모든 메서드를 구현합니다.

1. Advertising Factory를 통해 TVSDK에서 사용할 정책 인스턴스를 할당합니다.

>[!IMPORTANT]
>
>MediaPlayer 인스턴스가 >할당 해제되면 >재생 시작 시 등록된 사용자 지정 광고 정책은 지워집니다.새 재생 세션이 생성될 때마다 애플리케이션이 정책 >선택기 인스턴스를 등록해야 합니다.

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

1. 맞춤화 구현.
