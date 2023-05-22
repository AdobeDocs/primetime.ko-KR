---
description: MediaPlayer에서는 초기 버퍼링 시간 및 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.
title: 버퍼링 시간 설정
exl-id: d2fbae05-2190-4acc-ae63-561db030608a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 버퍼링 시간 설정{#set-buffering-times}

MediaPlayer에서는 초기 버퍼링 시간 및 재생 버퍼링 시간을 설정하고 가져오는 메서드를 제공합니다.

>[!TIP]
>
>재생을 시작하기 전에 버퍼 제어 매개 변수를 설정하지 않으면 미디어 플레이어의 기본값은 초기 버퍼의 경우 2초, 진행 중인 재생 버퍼 시간의 경우 30초로 설정됩니다.

1. 다음을 설정합니다. `BufferControlParameters` 초기 버퍼 시간 및 재생 버퍼 시간 제어 매개 변수를 캡슐화하는 개체:

       이 클래스는 다음과 같은 팩터리 메서드를 제공합니다.
   
   * 초기 버퍼 시간을 재생 버퍼 시간과 동일하게 설정하려면 다음을 수행합니다.

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * 초기 및 재생 버퍼 시간을 모두 설정하려면 다음을 수행합니다.

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      이 메서드는 `IllegalArgumentException` 매개 변수가 유효하지 않은 경우(예: 다음과 같은 경우)

   * 초기 버퍼 시간은 0보다 작습니다.
   * 초기 버퍼 시간은 버퍼 시간보다 크다.

1. 버퍼 매개 변수 값을 설정하려면 다음을 사용합니다. `MediaPlayer` 방법:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. 현재 버퍼 매개 변수 값을 가져오려면 다음을 사용합니다. `MediaPlayer` 방법:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

예를 들어 초기 버퍼를 2초로 설정하고 재생 버퍼 시간을 30초로 설정하려면 다음을 수행합니다.

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

다음 `psdkdemo` 이 기능을 보여 줍니다. 응용 프로그램의 설정을 사용하여 버퍼 값을 설정하십시오.
