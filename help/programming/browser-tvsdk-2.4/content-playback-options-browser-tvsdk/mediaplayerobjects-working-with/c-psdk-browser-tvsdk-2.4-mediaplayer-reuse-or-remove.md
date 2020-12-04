---
description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.
seo-description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.
seo-title: MediaPlayer 인스턴스 재사용 또는 제거
title: MediaPlayer 인스턴스 재사용 또는 제거
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# MediaPlayer 인스턴스 재사용 또는 제거{#reuse-or-remove-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

## MediaPlayer 인스턴스 {#section_C183E6164C184C3CBC5321FC6A2528EA} 재설정 또는 재사용

`MediaPlayer` 인스턴스를 재설정하여 `MediaPlayerStatus`에 정의된 대로 초기화되지 않은 IDLE 상태로 되돌릴 수 있습니다. 현재 미디어 항목을 교체하거나 이전에 불러온 미디어 리소스를 사용하여 새 미디어 항목을 설정할 수도 있습니다.

이 작업은 다음 경우에 유용합니다.

* `MediaPlayer` 인스턴스를 재사용하려는 경우 새 `MediaResource`(비디오 컨텐츠)을 로드하고 이전 인스턴스를 바꿔야 합니다.

   재설정을 사용하면 리소스를 해제하거나 `MediaPlayer`을(를) 다시 만들고 리소스를 다시 할당하는 등의 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 수 있습니다. `replaceCurrentItem` 메서드는 자동으로 이러한 단계를 수행합니다.

* `MediaPlayer`이(가) ERROR 상태이므로 지워야 할 때.

   >[!IMPORTANT]
   >
   >ERROR 상태에서 복구할 수 있는 유일한 방법입니다.

1. `MediaPlayer.reset()`을(를) 호출하여 `MediaPlayer` 인스턴스를 초기화되지 않은 상태로 되돌립니다.

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. `MediaPlayer.replaceCurrentItem()`을(를) 호출하여 다른 `MediaResource`

   >[!TIP]
   >
   >오류를 지우려면 동일한 `MediaResource`을(를) 로드하십시오.

1. `prepareToPlay()` 메서드를 호출합니다.

   >[!NOTE]
   >
   >준비된 상태 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 이벤트를 받으면 재생을 시작할 수 있습니다.

## MediaPlayer 인스턴스 및 리소스 {#section_2D159975C82245098E7078FE0B1578CE} 해제

MediaResource가 더 이상 필요하지 않은 경우 `MediaPlayer` 인스턴스와 리소스를 해제해야 합니다.

다음은 `MediaPlayer`을(를) 해제해야 하는 몇 가지 이유입니다.

* 불필요한 리소스를 보유하는 것은 성능에 영향을 줄 수 있습니다.
* 불필요한 `MediaPlayer` 개체를 방치하면 모바일 장치에 대한 지속적인 배터리 소모가 발생할 수 있습니다.
* 한 장치에서 동일한 비디오 코덱의 여러 인스턴스가 지원되지 않는 경우 다른 응용 프로그램에서 재생 오류가 발생할 수 있습니다.

* `MediaPlayer`을(를) 해제합니다.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >`MediaPlayer` 인스턴스가 릴리스되면 더 이상 사용할 수 없습니다. `MediaPlayer` 인터페이스의 어떤 메서드도 실행 후 호출되면 `IllegalStateException`이 발생합니다.

