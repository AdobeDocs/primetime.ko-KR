---
description: 일부 분석 구현에서 클라이언트 응용 프로그램은 TVSDK의 localTime 값으로 보고되는 위치와 다른 재생 헤드 위치를 제공하려고 할 수 있습니다. 예를 들어 선형 스트림 재생 중에 각 프로그램의 재생 헤드를 시작 시간과 관련하여 제공할 수 있습니다.
title: 사용자 지정 시간 업데이트 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# 사용자 지정 시간 업데이트 구현{#implement-custom-time-updates}

일부 분석 구현에서 클라이언트 응용 프로그램은 TVSDK의 localTime 값으로 보고되는 위치와 다른 재생 헤드 위치를 제공하려고 할 수 있습니다. 예를 들어 선형 스트림 재생 중에 각 프로그램의 재생 헤드를 시작 시간과 관련하여 제공할 수 있습니다.

>[!TIP]
>
>기본 위치와 다른 재생 헤드 위치를 제공하려는 경우에만 이 메서드를 재정의합니다.

1. 기본 재생 헤드 위치를 재정의하려면

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >이 코드 샘플에서 500은 샘플 값일 뿐입니다. 사용자 정의 재생 헤드 위치에 다른 값을 사용해야 합니다.

