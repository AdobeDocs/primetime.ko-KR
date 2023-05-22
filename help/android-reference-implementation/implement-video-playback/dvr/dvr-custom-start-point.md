---
description: ConfigProvider 클래스를 사용하여 처음에 DVR 스트림을 입력하는 기본 동작 대신 언제 DVR 스트림을 입력할지 지정할 사용자 지정 시작점을 선택할 수 있습니다.
title: DVR의 사용자 지정 시작 지점 선택
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# DVR의 사용자 지정 시작 지점 선택 {#choosing-a-custom-starting-point-for-dvr}

ConfigProvider 클래스를 사용하여 처음에 DVR 스트림을 입력하는 기본 동작 대신 언제 DVR 스트림을 입력할지 지정할 사용자 지정 시작점을 선택할 수 있습니다.

다음을 통해 시작 시간을 설정하려면 [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 클래스:

1. 사용 [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. 시작 시간 설정 [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. 사용자 정의 시작 위치가 활성화되어 있는지 확인합니다.
