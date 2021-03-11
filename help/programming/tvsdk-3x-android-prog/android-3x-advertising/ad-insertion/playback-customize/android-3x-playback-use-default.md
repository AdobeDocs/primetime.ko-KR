---
description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
title: 기본 재생 동작 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# 기본 재생 동작 사용 {#use-the-default-playback-behavior}

기본 광고 동작을 사용하도록 선택할 수 있습니다.

1. 기본 동작을 사용하려면 다음 작업 중 하나를 완료하십시오.

   * 자체 `AdvertisingFactory` 클래스를 구현하는 경우 `createAdPolicySelector`에 대해 null을 반환합니다.

   * `AdvertisingFactory` 클래스에 대한 사용자 정의 구현이 없는 경우 TVSDK는 기본 광고 정책 선택기를 사용합니다.

## 사용자 지정된 재생 {#set-up-customized-playback} 설정

광고 동작을 사용자 정의하거나 재정의할 수 있습니다.

광고 행동을 사용자 정의하거나 무시하려면 먼저 에 광고 정책 인스턴스를 등록합니다.
광고 동작을 사용자 정의하려면 다음 중 하나를 수행합니다.

* `AdPolicySelector` 인터페이스와 모든 메서드를 구현합니다.

   이 옵션은 기본 광고 비헤이비어를 **모두**&#x200B;로 재정의해야 하는 경우에 좋습니다.

* `DefaultAdPolicySelector` 클래스를 확장하고 사용자 지정이 필요한 비헤이비어에 대해서만 구현을 제공합니다.

   이 옵션은 기본 비헤이비어의 **일부**&#x200B;만 재정의해야 하는 경우에 좋습니다.

광고 비헤이비어를 사용자 정의하려면

1. `AdPolicySelector` 인터페이스와 모든 메서드를 구현합니다.
1. 광고 공장을 통해 TVSDK에서 사용할 정책 인스턴스를 지정합니다.

   >[!NOTE]
   >
   >class CustomContentFactory는 ContentFactory &amp;lbrace;를 확장합니다.
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>(MediaPlayerItem mediaPlayerItem) amp;lbrace;
   >새 CustomAdPolicySelector(mediaPlayerItem);를 반환합니다.
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >// 사용자 정의 컨텐츠 팩토리를 미디어 플레이어에 등록
   >MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// 리소스를 로드하는 동안 이 구성이 나중에 전달되어야 합니다.
   >mediaPlayer.replaceCurrentResource(resource, config);

1. 사용자 정의 구현
