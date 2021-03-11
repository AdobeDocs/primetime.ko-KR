---
description: MediaPlayer는 초기 버퍼링 시간과 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.
title: 버퍼링 시간 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# 버퍼링 시간 설정{#set-buffering-times}

MediaPlayer는 초기 버퍼링 시간과 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.

>[!TIP]
>
>재생을 시작하기 전에 버퍼 컨트롤 매개 변수를 설정하지 않으면 미디어 플레이어의 기본값은 초기 버퍼의 경우 2초로 설정되며, 진행 중인 재생 버퍼 시간의 경우 30초로 설정됩니다.

1. 초기 버퍼 시간 및 재생 버퍼 시간 제어 매개 변수를 캡슐화하는 `BufferControlParameters` 객체를 설정합니다.

       이 클래스는 다음과 같은 팩토리 메서드를 제공합니다.
   
   * 초기 버퍼 시간을 재생 버퍼 시간과 동일하게 설정하려면:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * 초기 및 재생 버퍼 시간을 모두 설정하려면:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      다음 경우와 같이 매개 변수가 올바르지 않으면 이 메서드는 `IllegalArgumentException`을 실행합니다.

   * 초기 버퍼 시간이 0보다 작습니다.
   * 초기 버퍼 시간이 버퍼 시간보다 큽니다.

1. 버퍼 매개 변수 값을 설정하려면 다음 `MediaPlayer` 메서드를 사용합니다.

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. 현재 버퍼 매개 변수 값을 가져오려면 다음 `MediaPlayer` 메서드를 사용합니다.

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

예를 들어 초기 버퍼를 2초로 설정하고 재생 버퍼 시간을 30초로 설정하려면:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

`psdkdemo`에서 이 기능을 보여 줍니다.응용 프로그램의 설정을 사용하여 버퍼 값을 설정합니다.
