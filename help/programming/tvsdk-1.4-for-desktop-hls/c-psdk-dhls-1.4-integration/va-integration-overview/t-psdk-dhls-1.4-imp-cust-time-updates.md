---
description: 특정 분석 구현에서 클라이언트 응용 프로그램은 TVSDK localTime 값에 의해 보고된 것과 다른 재생 헤드 위치를 제공하려고 할 수 있습니다. 예를 들어 선형 스트림 재생 중에 각 프로그램의 재생 헤드를 시작 시간과 관련하여 제공할 수 있습니다.
seo-description: 특정 분석 구현에서 클라이언트 응용 프로그램은 TVSDK localTime 값에 의해 보고된 것과 다른 재생 헤드 위치를 제공하려고 할 수 있습니다. 예를 들어 선형 스트림 재생 중에 각 프로그램의 재생 헤드를 시작 시간과 관련하여 제공할 수 있습니다.
seo-title: 사용자 지정 시간 업데이트 구현
title: 사용자 지정 시간 업데이트 구현
uuid: 2b46eca9-3815-4c44-ab5e-21678c35f410
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 사용자 지정 시간 업데이트 구현{#implement-custom-time-updates}

특정 분석 구현에서 클라이언트 응용 프로그램은 TVSDK localTime 값에 의해 보고된 것과 다른 재생 헤드 위치를 제공하려고 할 수 있습니다. 예를 들어 선형 스트림 재생 중에 각 프로그램의 재생 헤드를 시작 시간과 관련하여 제공할 수 있습니다.

>[!TIP]
>
>기본 위치가 아닌 다른 재생 헤드 위치를 제공하려는 경우에만 이 메서드를 재정의합니다.

1. 기본 재생 헤드 위치를 재정의하려면

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
   >이 코드 조각에 있는 값은 샘플입니다. 사용자 정의 재생 헤드 위치에 다른 값을 사용해야 합니다.

