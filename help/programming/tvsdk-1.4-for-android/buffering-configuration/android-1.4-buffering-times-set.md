---
description: 더 원활한 보기 환경을 제공하기 위해 TVSDK는 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.
title: 버퍼링 시간 설정
exl-id: 4542d10a-b6f8-430d-8b9a-5a358d1c0e9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 버퍼링 {#buffering}

더 원활한 보기 환경을 제공하기 위해 TVSDK는 비디오 스트림을 버퍼링하는 경우가 있습니다. 플레이어가 버퍼링하는 방식을 구성할 수 있습니다.

TVSDK는 최소 30초의 재생 버퍼 길이와 미디어 재생이 시작되기 전 최소 2초의 초기 버퍼 시간을 정의합니다. 응용 프로그램 호출 후 `play` 그러나 재생이 시작되기 전에 TVSDK는 미디어를 초기 시간까지 버퍼링하여 실제로 재생을 시작할 때 매끄럽게 시작합니다.

새 버퍼링 정책을 정의하여 버퍼 시간을 변경할 수 있으며 인스턴트 온을 사용하여 초기 버퍼링 발생 시기를 변경할 수 있습니다.

## 버퍼링 시간 설정 {#set-buffering-times}

다음 `MediaPlayer` 는 초기 버퍼링 시간 및 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.

>[!TIP]
>
>재생을 시작하기 전에 버퍼 제어 매개 변수를 설정하지 않으면 미디어 플레이어의 기본값은 초기 버퍼의 경우 2초, 진행 중인 재생 버퍼 시간의 경우 30초로 설정됩니다.

1. 다음을 설정합니다. `BufferControlParameters` 초기 버퍼 시간 및 재생 버퍼 시간 제어 매개 변수를 캡슐화하는 개체:

       이 클래스는 두 가지 팩터리 메서드를 제공합니다.
   
   * 초기 버퍼 시간을 재생 버퍼 시간과 동일하게 설정하려면 다음을 수행합니다.

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * 초기 및 재생 버퍼 시간을 모두 설정하려면 다음을 수행합니다.

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      이 메서드는 `IllegalArgumentException` 매개 변수가 유효하지 않은 경우(예: 다음과 같은 경우)

   * 초기 버퍼 시간은 0보다 작습니다.
   * 초기 버퍼 시간은 버퍼 시간보다 크다.

1. 버퍼 매개 변수 값을 설정하려면 다음을 사용합니다. `MediaPlayer` 방법:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 현재 버퍼 매개 변수 값을 가져오려면 다음을 사용합니다. `MediaPlayer` 방법:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   AVE에서 지정된 값을 설정할 수 없으면 미디어 플레이어가 `ERROR` 오류 코드가 있는 상태 `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

예를 들어 초기 버퍼를 2초로 설정하고 재생 버퍼 시간을 30초로 설정하려면 다음을 수행합니다.

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetime 참조 구현은 이 기능을 보여 줍니다. 애플리케이션의 설정을 사용하여 버퍼 값을 설정하십시오.
