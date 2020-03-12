---
description: 보다 매끄러운 보기 환경을 제공하기 위해 TVSDK가 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.
seo-description: 보다 매끄러운 보기 환경을 제공하기 위해 TVSDK가 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.
seo-title: 버퍼링
title: 버퍼링
uuid: c84b98ed-0070-4a86-a409-d7702e5be23c
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 개요 {#buffering-overview}

보다 매끄러운 보기 환경을 제공하기 위해 TVSDK가 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.

TVSDK는 최소 30초의 재생 버퍼 길이와 미디어 재생이 시작되기 전의 초기 버퍼 시간을 최소 2초로 정의합니다. 응용 프로그램이 호출된 `play`후 재생이 시작되기 전에 TVSDK는 미디어를 초기 시간까지 버퍼링하여 실제로 재생을 시작할 때 매끄럽게 시작합니다.

새로운 버퍼링 정책을 정의하여 버퍼 시간을 변경할 수 있으며, 초기 버퍼링이 발생하는 경우 즉시 사용

## 버퍼링 시간 정책 {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

환경(장치, 운영 체제 또는 네트워크 조건 포함)에 따라 초기 버퍼링에 대한 최소 지속 시간 변경과 진행 중인 재생 버퍼링에 대한 등 플레이어에 대해 다른 버퍼링 정책을 설정할 수 있습니다.

호출한 `play`후 미디어 플레이어는 비디오를 버퍼링하기 시작합니다. 미디어 플레이어가 초기 버퍼 시간으로 지정된 비디오 양을 버퍼링하면 재생이 시작됩니다. 플레이어는 재생을 시작하기 전에 전체 재생 버퍼가 채워질 때까지 기다리지 않으므로 시작 시간이 향상됩니다. 대신 초기 몇 초가 버퍼링된 후 재생이 시작됩니다.

비디오가 렌더링되는 동안 TVSDK는 재생 버퍼 시간으로 지정된 양을 버퍼링할 때까지 새로운 조각을 계속 버퍼링합니다. 현재 버퍼 길이가 재생 버퍼 시간 아래로 떨어지면 플레이어는 추가 조각을 다운로드합니다. 현재 버퍼 길이가 몇 초 정도 재생 버퍼 시간을 초과하면 TVSDK는 조각 다운로드를 중지합니다.

>[!TIP]
>
>초기 버퍼 값이 높은 경우 시작하기 전에 사용자에게 긴 초기 버퍼링 시간을 줄 수 있습니다. 그러면 더 오랫동안 매끄럽게 재생할 수 있습니다.그러나 네트워크 상태가 좋지 않으면 초기 재생이 지연될 수 있습니다.

호출로 즉시 켜짐으로써 `prepareBuffer`활성화하면 초기 버퍼링이 기다리지 않고 그 순간에 시작됩니다 `play`.

## 버퍼링 시간 설정 {#section_05CDD927869D47EBA1D2069B1416B2E4}

이 `MediaPlayer` 예제에서는 초기 버퍼링 시간과 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.

>[!TIP]
>
>재생을 시작하기 전에 버퍼 컨트롤 매개 변수를 설정하지 않으면 미디어 플레이어의 기본값은 초기 버퍼의 경우 2초이고 진행 중인 재생 버퍼 시간의 경우 30초입니다.

1. 초기 버퍼 시간 및 재생 버퍼 시간 제어 매개 변수를 캡슐화하는 `BufferControlParameters` 개체를 설정합니다.

   이 클래스는 다음과 같은 공장 메서드를 제공합니다.

   * 초기 버퍼 시간을 재생 버퍼 시간과 같게 설정하려면

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * 초기 및 재생 버퍼 시간을 설정하려면

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   매개 변수가 올바르지 않으면 다음 조건을 충족하는 경우와 같이 이러한 메서드는 오류 `MediaPlayerException` 코드와 함께 `PSDKErrorCode.INVALID_ARGUMENT`실행됩니다.

   * 초기 버퍼 시간이 0보다 작습니다.
   * 초기 버퍼 시간이 버퍼 시간보다 큽니다.


1. 버퍼 매개 변수 값을 설정하려면 다음 `MediaPlayer` 방법을 사용합니다.

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 현재 버퍼 매개 변수 값을 가져오려면 다음 `MediaPlayer` 방법을 사용합니다.

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

예를 들어 초기 버퍼를 5초로 설정하고 재생 버퍼 시간을 30초로 설정하려면:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
