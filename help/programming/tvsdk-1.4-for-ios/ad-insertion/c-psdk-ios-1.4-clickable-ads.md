---
description: TVSDK는 클릭스루 광고에 대한 작업을 수행할 수 있도록 정보를 제공합니다. 플레이어 UI를 만들 때 사용자가 클릭 가능한 광고를 클릭할 때 응답하는 방법을 결정해야 합니다.
seo-description: TVSDK는 클릭스루 광고에 대한 작업을 수행할 수 있도록 정보를 제공합니다. 플레이어 UI를 만들 때 사용자가 클릭 가능한 광고를 클릭할 때 응답하는 방법을 결정해야 합니다.
seo-title: 클릭 가능한 광고
title: 클릭 가능한 광고
uuid: dc02cba7-34ad-4c74-9ceb-2fc1050d54aa
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# 클릭 가능한 광고{#clickable-ads}

TVSDK는 클릭스루 광고에 대한 작업을 수행할 수 있도록 정보를 제공합니다. 플레이어 UI를 만들 때 사용자가 클릭 가능한 광고를 클릭할 때 응답하는 방법을 결정해야 합니다.

iOS용 TVSDK에서는 선형 광고만 클릭할 수 있습니다.

## 광고 {#section_537AF2593FDB4257B81AAE2103B0C719} 클릭 수에 응답

사용자가 광고, 컴패니언 배너 광고 또는 관련 버튼을 클릭하면 애플리케이션이 응답해야 합니다. TVSDK는 클릭의 대상 URL에 대한 정보를 제공합니다.

1. TVSDK에 대한 이벤트 수신기를 설정하고 클릭스루 정보를 제공하려면 `PTMediaPlayerAdClickNotification`에 대한 관찰자를 추가하십시오.

   >[!NOTE]
   >
   >사용자가 광고, 컴패니언 배너 광고 또는 관련 단추를 클릭하면 TVSDK가 클릭 대상에 대한 정보를 포함하여 이 알림을 전달합니다.

1. 클릭 가능한 광고에서 사용자 상호 작용을 모니터링합니다.
1. 사용자가 광고 또는 단추를 터치하거나 클릭하는 경우 TVSDK에 알리려면 `[_player notifyClick:_currentAd.primaryAsset];`을 사용하십시오.
1. TVSDK에서 `PTMediaPlayerAdClickNotification` 이벤트를 수신합니다.
1. 클릭스루 URL 및 관련 정보를 검색하려면 `PTMediaPlayerAdClickURLKey` 개체를 사용하십시오.
1. 비디오를 일시 중지합니다.
1. 클릭스루 정보를 사용하여 광고 클릭스루 URL과 관련 정보를 표시합니다.

   >[!NOTE]
   >
   >예를 들어 다음 방법 중 하나로 정보를 표시할 수 있습니다.

   * 브라우저에서 클릭스루 URL을 열어 응용 프로그램에서 선택합니다.

      데스크톱 플랫폼에서 비디오 광고 재생 영역은 사용자 클릭 시 클릭스루 URL을 호출하는 데 사용됩니다.
   * 사용자를 외부 모바일 웹 브라우저로 리디렉션합니다.

      모바일 장치에서 비디오 광고 재생 영역은 컨트롤 숨기기 및 표시, 재생 일시 중지, 전체 화면으로 확장 등과 같은 다른 기능에 사용됩니다. 이러한 장치에서는 스폰서 버튼과 같은 별도의 보기를 사용하여 클릭스루 URL을 실행합니다.

1. 클릭스루 정보가 표시되는 브라우저 창을 닫고 비디오 재생을 다시 시작합니다.

   예:

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   ```

