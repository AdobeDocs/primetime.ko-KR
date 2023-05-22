---
description: 광고 삽입 메타데이터를 사용자 지정할 수 있습니다.
title: 광고 삽입 메타데이터 사용자 지정
exl-id: 4881ace6-e97b-448d-8fb4-64e7b69517f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 광고 삽입 메타데이터 사용자 지정{#customize-ad-insertion-metadata}

광고 삽입 메타데이터를 사용자 지정할 수 있습니다.

1. 해결되지 않은 기회에 대한 광고 메타데이터에 대한 시간 제한을 설정하십시오.

   이 시간 초과에 대한 기본값은 20초입니다.
1. 값을 10초로 변경하려면 다음을 입력합니다.

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   다음 `timeout` 속성이에 정의됨 `AdvertisingMetadata` 클래스에서 파생되는 모든 사용자 지정 광고 설정에 대해 이 시간 제한을 설정할 수 있습니다. `AdvertisingMetadata` 클래스. 예를 들어 사용자가 FreeWheel 확인자에 대한 사용자 지정 설정을 정의하는 경우 이 설정을 사용하여 기본 시간 초과를 설정할 수 있습니다.

1. 만들기 `MediaPlayerItemConfig` (2단계의 광고 설정 포함)

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 호출 시 이 구성 사용 `replaceCurrentResource` 날짜 `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
