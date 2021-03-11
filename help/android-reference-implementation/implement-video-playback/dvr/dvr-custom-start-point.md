---
description: ConfigProvider 클래스를 사용하여 시작할 때 DVR 스트림을 입력하는 기본 동작 대신 DVR 스트림을 입력할 때의 사용자 지정 시작점을 선택할 수 있습니다.
title: DVR에 대한 사용자 정의 시작 지점 선택
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# DVR {#choosing-a-custom-starting-point-for-dvr}에 대한 사용자 정의 시작 지점 선택

ConfigProvider 클래스를 사용하여 시작할 때 DVR 스트림을 입력하는 기본 동작 대신 DVR 스트림을 입력할 때의 사용자 지정 시작점을 선택할 수 있습니다.

시작 시간을 [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 클래스에서 설정하려면:

1. [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled())를 활성화합니다.
1. 시작 시간을 [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref())에서 설정합니다.
1. 사용자 지정 시작 위치가 활성화되어 있는지 확인합니다.
