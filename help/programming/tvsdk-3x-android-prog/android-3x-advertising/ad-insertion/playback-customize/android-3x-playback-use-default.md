---
description: 기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.
title: 기본 재생 동작 사용
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 기본 재생 동작 사용 {#use-the-default-playback-behavior}

기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.

1. 기본 동작을 사용하려면 다음 작업 중 하나를 완료하십시오.

   * 자체 를 구현하는 경우 `AdvertisingFactory` class, 다음에 대해 null 반환: `createAdPolicySelector`.

   * 에 대한 사용자 지정 구현이 없는 경우 `AdvertisingFactory` 클래스, TVSDK는 기본 광고 정책 선택기를 사용합니다.

## 사용자 지정 재생 설정 {#set-up-customized-playback}

광고 비헤이비어를 사용자 정의하거나 재정의할 수 있습니다.

광고 동작을 사용자 정의하거나 재정의하려면 먼저 광고 정책 인스턴스를( )에 등록합니다.
광고 동작을 사용자 지정하려면 다음 중 하나를 수행하십시오.

* 구현 `AdPolicySelector` 인터페이스 및 모든 해당 메서드.

  재정의해야 하는 경우 이 옵션을 권장합니다. **모두** 기본 광고 동작입니다.

* 확장 `DefaultAdPolicySelector` 클래스를 만들고 맞춤화가 필요한 비헤이비어에 대해서만 구현을 제공합니다.

  이 옵션은 재정의해야 하는 경우에만 권장됩니다. **일부** 기본 동작.

광고 비헤이비어를 사용자 지정하려면:

1. 구현 `AdPolicySelector` 인터페이스 및 모든 해당 메서드를 사용합니다.
1. Advertising Factory를 통해 TVSDK에서 사용할 정책 인스턴스를 할당합니다.

   >[!NOTE]
   >
   >클래스 CustomContentFactory가 ContentFactory &amp;lbrace;를 확장합니다.
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >새 CustomAdPolicySelector(mediaPlayerItem) 반환;
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >// 미디어 플레이어에 사용자 지정 콘텐츠 팩토리 등록
   >MediaPlayerItemConfig = 새 MediaPlayerItemConfig();
   >config.setAdvertisingFactory(새로운 CustomContentFactory());
   >// >리소스를 로드하는 동안 이 구성을 나중에 전달해야 합니다.
   >mediaPlayer.replaceCurrentResource(resource, config);

1. 맞춤화 구현.
