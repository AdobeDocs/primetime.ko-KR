---
description: ConfigProvider 클래스를 사용하여 시작할 때 DVR 스트림을 입력하는 기본 동작 대신 DVR 스트림에 입장할 때의 사용자 지정 시작점을 선택할 수 있습니다.
seo-description: ConfigProvider 클래스를 사용하여 시작할 때 DVR 스트림을 입력하는 기본 동작 대신 DVR 스트림에 입장할 때의 사용자 지정 시작점을 선택할 수 있습니다.
seo-title: DVR에 대한 사용자 정의 시작 지점 선택
title: DVR에 대한 사용자 정의 시작 지점 선택
uuid: a7e13865-2b86-4234-ac4c-9a5320b293db
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# DVR에 대한 사용자 정의 시작 지점 선택 {#choosing-a-custom-starting-point-for-dvr}

ConfigProvider 클래스를 사용하여 시작할 때 DVR 스트림을 입력하는 기본 동작 대신 DVR 스트림에 입장할 때의 사용자 지정 시작점을 선택할 수 있습니다.

ConfigProvider 클래스를 통해 시작 [시간을 설정하려면](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 다음을 수행합니다.

1. isCustomPositionPrefEnabled() [를 활성화합니다](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. retrieveStartTimePref() [에서 시작 시간을 설정합니다](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. 사용자 지정 시작 위치가 활성화되어 있는지 확인합니다.
