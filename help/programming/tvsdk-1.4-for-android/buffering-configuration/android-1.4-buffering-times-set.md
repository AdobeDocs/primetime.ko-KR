---
description: 보다 매끄러운 보기 환경을 제공하기 위해 TVSDK가 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.
seo-description: 보다 매끄러운 보기 환경을 제공하기 위해 TVSDK가 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.
seo-title: 버퍼링 시간 설정
title: 버퍼링 시간 설정
uuid: 5a3945a4-1935-4797-b19d-84989850a487
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 버퍼링 {#buffering}

보다 매끄러운 보기 환경을 제공하기 위해 TVSDK가 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.

TVSDK는 최소 30초의 재생 버퍼 길이와 미디어 재생 시작 전 최소 2초의 초기 버퍼 시간을 정의합니다. 애플리케이션을 호출한 `play` 후 재생이 시작되기 전에 TVSDK는 미디어를 초기 시간까지 버퍼링하여 실제로 재생을 시작할 때 매끄럽게 시작합니다.

새로운 버퍼링 정책을 정의하여 버퍼 시간을 변경할 수 있으며, 인스턴트 온을 사용하여 초기 버퍼링이 발생하는 시기를 변경할 수 있습니다.

## 버퍼링 시간 설정 {#set-buffering-times}

이 `MediaPlayer` 예제에서는 초기 버퍼링 시간과 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.

>[!TIP]
>
>재생을 시작하기 전에 버퍼 컨트롤 매개 변수를 설정하지 않으면 미디어 플레이어의 기본값은 초기 버퍼의 경우 2초이고 진행 중인 재생 버퍼 시간의 경우 30초입니다.

1. 초기 버퍼 시간 및 재생 버퍼 시간 제어 매개 변수를 캡슐화하는 `BufferControlParameters` 객체를 설정합니다.

       이 클래스는 다음과 같은 두 가지 팩토리 메서드를 제공합니다.
   
   * 초기 버퍼 시간을 재생 버퍼 시간과 같게 설정하려면

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * 초기 및 재생 버퍼 시간을 모두 설정하려면

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      이러한 메서드는 다음과 같이 매개 변수가 유효하지 않은 `IllegalArgumentException` 경우

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

   AVE가 지정된 값을 설정할 수 없는 경우 미디어 플레이어는 오류 코드와 함께 `ERROR` 상태로 `SET_BUFFER_PARAMETERS_ERROR`들어갑니다.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

예를 들어 초기 버퍼를 2초로 설정하고 재생 버퍼 시간을 30초로 설정하려면:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetime 참조 구현에서 이 기능을 시연합니다.응용 프로그램의 설정을 사용하여 버퍼 값을 설정합니다.