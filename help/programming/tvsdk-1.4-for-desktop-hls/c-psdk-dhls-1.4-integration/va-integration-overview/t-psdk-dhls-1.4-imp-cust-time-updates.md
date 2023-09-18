---
description: 특정 분석 구현에서, 클라이언트 애플리케이션은 TVSDK localTime 값에 의해 보고된 것과 다른 플레이헤드 위치를 제공하기를 원할 수 있다. 예를 들어, LINEAR 스트림 재생 중에 각 프로그램의 플레이헤드가 그 시작 시간을 기준으로 제공될 수 있다.
title: 사용자 지정 시간 업데이트 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 사용자 지정 시간 업데이트 구현{#implement-custom-time-updates}

특정 분석 구현에서, 클라이언트 애플리케이션은 TVSDK localTime 값에 의해 보고된 것과 다른 플레이헤드 위치를 제공하기를 원할 수 있다. 예를 들어, LINEAR 스트림 재생 중에 각 프로그램의 플레이헤드가 그 시작 시간을 기준으로 제공될 수 있다.

>[!TIP]
>
>기본 위치가 아닌 다른 플레이헤드 위치를 제공하려는 경우에만 이 메서드를 재정의합니다.

1. 기본 플레이헤드 위치를 재정의하려면

   ```
   vaMetadata.currentTimeUpdateBlock = function():Number { 
      if (currentTime == 0) { 
          currentTime = getTimer(); 
      } 
      return ((getTimer() - currentTime) / 1000 + 1000); 
   }
   ```

   >[!IMPORTANT]
   >
   >이 코드 조각의 값은 샘플일 뿐입니다. 사용자 지정 플레이헤드 위치에 다른 값을 사용해야 합니다.
