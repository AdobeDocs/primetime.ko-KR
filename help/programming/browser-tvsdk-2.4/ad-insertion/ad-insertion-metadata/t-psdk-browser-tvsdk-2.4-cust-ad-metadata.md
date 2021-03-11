---
description: 광고 삽입 메타데이터를 사용자 정의할 수 있습니다.
title: 광고 삽입 메타데이터 사용자 정의
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 광고 삽입 메타데이터 사용자 지정{#customize-ad-insertion-metadata}

광고 삽입 메타데이터를 사용자 정의할 수 있습니다.

1. 해결되지 않은 기회에 대한 광고 메타데이터에 대한 제한 시간을 설정합니다.

   이 시간 초과의 기본값은 20초입니다.
1. 값을 10초로 변경하려면 다음을 입력합니다.

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   `timeout` 속성은 `AdvertisingMetadata` 클래스에 정의되며 이 시간 초과는 `AdvertisingMetadata` 클래스에서 파생되는 모든 사용자 지정 광고 설정에 대해 설정할 수 있습니다. 예를 들어 사용자가 FreeWheel 확인자에 대한 사용자 정의 설정을 정의하는 경우 이 설정을 사용하여 기본 시간 제한을 설정할 수 있습니다.

1. 2단계에서 광고 설정으로 `MediaPlayerItemConfig`을 만듭니다.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. `MediaPlayer`에서 `replaceCurrentResource`을(를) 호출할 때 이 구성을 사용합니다.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

