---
title: 콘솔 앱 로그를 사용하여 AccessEnabler iOS/tvOS SDK 디버깅
description: 콘솔 앱 로그를 사용하여 AccessEnabler iOS/tvOS SDK 디버깅
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# 콘솔 앱 로그를 사용하여 AccessEnabler iOS/tvOS SDK 디버깅 {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.


## 개요

이 문서의 범위는 콘솔 앱 로그를 사용하여 AccessEnabler 프레임워크를 디버깅하는 데 유용한 세부 정보와 함께 AccessEnabler의 iOS/tvOS SDK 로깅 메커니즘을 캡처하고 제공하는 것입니다.

## 로깅 메커니즘 상태

AccessEnabler iOS/tvOS 로깅 메커니즘 목적은 AccessEnabler 프레임워크를 사용하는 응용 프로그램이 이로 인해 발생할 수 있는 문제를 해결하기 위해 유용한 메시지를 전송하는 것입니다.

### AccessEnabler iOS/tvOS 3.5.0 이상

AccessEnabler iOS/tvOS 3.5.0 버전부터 로깅 메커니즘은 다음과 같은 변경 사항을 도입합니다.

* AccessEnabler 프레임워크는 Apple에서 권장하는 기능을 사용합니다 [OSLog](https://developer.apple.com/documentation/os/oslog) 구현 을 참조하십시오.

* AccessEnabler 프레임워크는 하위 시스템에 따라 콘솔 앱 로그를 필터링하는 기능을 제공합니다. **com.adobe.pass.AccessEnabler**. SDK에서 내보내는 모든 메시지는 com.adobe.pass.AccessEnabler에 포함됩니다.

* AccessEnabler 프레임워크는 모든(접두사)을 기준으로 콘솔 앱 로그를 필터링하는 기능을 도입했습니다. **[AccessEnabler]**. SDK에서 보내는 모든 메시지에는 [AccessEnabler].

* AccessEnabler 프레임워크는 카테고리에 따라 콘솔 앱 로그를 필터링하는 기능을 제공합니다. **디버그**, **오류** 위의 두 가지 기준 중 하나와 함께 사용할 수 있습니다. 하위 시스템 또는 임의(접두사)

## 콘솔 앱 로그를 사용하여 디버깅

조사 중인 문제에 따라 AccessEnabler 프레임워크에서 제공하는 로깅 메시지를 포함하거나 제외할 수 있으므로, 조사 중 및 콘솔 앱 로그를 사용할 때 도움이 되는 유용한 세부 정보를 아래에서 확인할 수 있습니다.


### AccessEnabler iOS/tvOS 3.5.0 이상

#### 포함 {#including}

먼저 AccessEnabler 프레임워크에서 제공하는 로깅 메시지를 확인할 수 있습니다 **반드시** 아래 이미지에 표시된 대로 콘솔 앱의 작업 섹션에서 &quot;정보 메시지 포함&quot; 및 &quot;디버그 메시지 포함&quot;을 선택합니다.

![](assets/include-info-debug-msg.png)


AccessEnabler iOS/tvOS SDK의 기능을 디버깅하기 위해 **참조** AccessEnabler 프레임워크 로그를 사용하여 다음을 수행할 수 있습니다.

* 를 사용하여 콘솔 앱에서 검색 **하위 시스템** 아래 그림과 같이 com.adobe.pass.AccessEnabler 값과 같은 옵션입니다.

![](assets/subsys-console-app.png)

* 를 사용하여 콘솔 앱에서 검색 **임의** 다음을 포함하는 옵션
   [AccessEnabler] 값을 사용할 수 없습니다.

![](assets/any-optn-console-app.png)

위의 두 가지 기준과 함께 를 사용할 수도 있습니다 **카테고리** 옵션 **하위 시스템** 또는 **임의(접두사)** 을 명시적으로 검색하는 **디버그** 또는 **오류** AccessEnabler iOS/tvOS SDK에서 내보내는 레벨 메시지입니다.

#### 제외

다른 구성 요소의 기능을 더 잘 디버깅하기 위해 **제외** AccessEnabler 프레임워크 로그를 사용하여 다음을 수행할 수 있습니다.

* 를 사용하여 콘솔 앱에서 검색 **하위 시스템** 이 옵션은 com.adobe.pass.AccessEnabler 값과 같지 않습니다.
* 를 사용하여 콘솔 앱에서 검색 **임의** 포함하지 않는 옵션 [AccessEnabler] 값.

## 문제 보고

Adobe Primetime 인증에 문제를 보고하는 경우 다음 제안을 고려하십시오.

* 복제 단계를 제공하십시오.
* 문제가 발생하는 OS 버전 및 장치 모델을 제공하십시오.
* 문제가 발생하는 AccessEnabler iOS/tvOS SDK 버전을 제공하십시오.
* 에 표시되는 두 옵션 중 하나를 사용하여 모든 AccessEnabler iOS/tvOS SDK 로깅 메시지를 캡처하고 첨부하십시오. [포함](#including) 섹션을 참조하십시오.
