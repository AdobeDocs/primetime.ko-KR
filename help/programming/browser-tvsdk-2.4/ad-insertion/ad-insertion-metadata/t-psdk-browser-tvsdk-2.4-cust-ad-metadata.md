---
description: 광고 삽입 메타데이터를 사용자 정의할 수 있습니다.
seo-description: 광고 삽입 메타데이터를 사용자 정의할 수 있습니다.
seo-title: 광고 삽입 메타데이터 사용자 정의
title: 광고 삽입 메타데이터 사용자 정의
uuid: 047470d3-45bd-48be-82ce-4e9d9fe6ea10
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 광고 삽입 메타데이터 사용자 정의{#customize-ad-insertion-metadata}

광고 삽입 메타데이터를 사용자 정의할 수 있습니다.

1. 해결되지 않은 기회에 대한 광고 메타데이터에 대한 제한 시간을 설정합니다.

   이 시간 제한의 기본값은 20초입니다.
1. 값을 10초로 변경하려면 다음을 입력합니다.

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   이 `timeout` 속성은 `AdvertisingMetadata` 클래스에서 정의되며, 이 시간 초과는 `AdvertisingMetadata` 클래스에서 파생되는 모든 사용자 지정 광고 설정에 대해 설정할 수 있습니다. 예를 들어 사용자가 FreeWheel 확인자에 대한 사용자 정의 설정을 정의하는 경우 이 설정을 사용하여 기본 시간 제한을 설정할 수 있습니다.

1. 2단계에서 광고 설정으로 `MediaPlayerItemConfig` 만듭니다.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 이 구성을 `replaceCurrentResource` 사용하여 `MediaPlayer`켜십시오.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

