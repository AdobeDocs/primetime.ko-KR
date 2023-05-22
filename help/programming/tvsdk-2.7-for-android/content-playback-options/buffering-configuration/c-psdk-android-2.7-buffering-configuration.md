---
description: 더 원활한 보기 환경을 제공하기 위해 TVSDK는 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.
title: 버퍼링
exl-id: f4df3084-376e-421c-aaa5-83de2815dabe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 개요 {#buffering-overview}

더 원활한 보기 환경을 제공하기 위해 TVSDK는 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.

TVSDK는 최소 30초의 재생 버퍼 길이와 미디어 재생이 시작되기 전 최소 2초의 초기 버퍼 시간을 정의합니다. 응용 프로그램 호출 후 `play`, 그러나 재생이 시작되기 전에 TVSDK는 미디어를 초기 시간까지 버퍼링하여 실제로 재생을 시작할 때 매끄럽게 시작합니다.

새 버퍼링 정책을 정의하여 버퍼 시간을 변경할 수 있으며 instant on을 사용하여 초기 버퍼링 발생 시기를 변경할 수 있습니다.

## 버퍼링 시간 정책 {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

환경(장치, 운영 체제 또는 네트워크 조건 포함)에 따라 플레이어에 대해 초기 버퍼링 및 지속적인 재생 버퍼링의 최소 기간 변경과 같은 다양한 버퍼링 정책을 설정할 수 있습니다.

통화 후 `play`에서 미디어 플레이어는 비디오 버퍼링을 시작합니다. 미디어 플레이어가 초기 버퍼 시간으로 지정된 비디오 양을 버퍼링하면 재생이 시작됩니다. 플레이어는 재생을 시작하기 전에 전체 재생 버퍼가 채워질 때까지 기다리지 않으므로 이 프로세스는 시작 시간을 향상시킵니다. 대신 초기 몇 초가 버퍼링되면 재생이 시작됩니다.

비디오가 렌더링되는 동안 TVSDK는 재생 버퍼 시간에 지정된 양을 버퍼링할 때까지 새 조각을 계속 버퍼링합니다. 현재 버퍼 길이가 재생 버퍼 시간 아래로 떨어지는 경우 플레이어는 추가 조각을 다운로드합니다. 현재 버퍼 길이가 재생 버퍼 시간보다 몇 초 초과되면 TVSDK는 조각 다운로드를 중지합니다.

>[!TIP]
>
>초기 버퍼 값이 높으면 시작하기 전에 사용자에게 긴 초기 버퍼링 시간을 제공할 수 있습니다. 이렇게 하면 더 긴 시간 동안 매끄러운 재생이 제공될 수 있지만, 네트워크 상태가 좋지 않으면 초기 재생이 지연될 수 있습니다.

를 호출하여 instant on을 활성화하면 `prepareBuffer`, 초기 버퍼링은 기다리지 않고 해당 시점에 시작됩니다. `play`.

## 버퍼링 시간 설정 {#section_05CDD927869D47EBA1D2069B1416B2E4}

다음 `MediaPlayer` 는 초기 버퍼링 시간 및 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.

>[!TIP]
>
>재생을 시작하기 전에 버퍼 제어 매개 변수를 설정하지 않으면 미디어 플레이어의 기본값은 초기 버퍼의 경우 2초, 진행 중인 재생 버퍼 시간의 경우 30초로 설정됩니다.

1. 다음을 설정합니다. `BufferControlParameters` object - 초기 버퍼 시간 및 재생 버퍼 시간 제어 매개 변수를 캡슐화합니다.

   이 클래스는 다음과 같은 팩터리 메서드를 제공합니다.

   * 초기 버퍼 시간을 재생 버퍼 시간과 동일하게 설정하려면 다음을 수행합니다.

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * 초기 및 재생 버퍼 시간을 설정하려면 다음을 수행합니다.

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   매개 변수가 올바르지 않으면 이 메서드는 throw합니다 `MediaPlayerException` 오류 코드 포함 `PSDKErrorCode.INVALID_ARGUMENT`: 다음 조건이 충족되는 경우와 같습니다.

   * 초기 버퍼 시간은 0보다 작습니다.
   * 초기 버퍼 시간은 버퍼 시간보다 크다.


1. 버퍼 매개 변수 값을 설정하려면 다음을 사용합니다 `MediaPlayer` 방법:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 현재 버퍼 매개 변수 값을 가져오려면 다음을 사용합니다. `MediaPlayer` 방법:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

예를 들어 초기 버퍼를 5초로 설정하고 재생 버퍼 시간을 30초로 설정하려면 다음을 수행합니다.

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
