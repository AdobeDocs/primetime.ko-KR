---
description: 일부 분석 구현에서 클라이언트 애플리케이션은 TVSDK의 localTime 값에 의해 보고되는 위치와는 다른 플레이헤드 위치를 제공하기를 원할 수 있다. 예를 들어, 선형 스트림 재생 중에, 각 프로그램의 플레이헤드가 그 시작 시간에 관하여 제공될 수 있다.
title: 사용자 지정 시간 업데이트 구현
exl-id: df35d422-d9dc-496d-8f6f-cf34d82ab046
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 사용자 지정 시간 업데이트 구현 {#implement-custom-time-updates}

일부 분석 구현에서 클라이언트 애플리케이션은 TVSDK의 localTime 값에 의해 보고되는 위치와는 다른 플레이헤드 위치를 제공하기를 원할 수 있다. 예를 들어, 선형 스트림 재생 중에, 각 프로그램의 플레이헤드가 그 시작 시간에 관하여 제공될 수 있다.

>[!TIP]
>
>기본 위치와 다른 플레이헤드 위치를 제공하려는 경우에만 이 메서드를 재정의합니다.

기본 플레이헤드 위치를 재정의하려면

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>이 코드 샘플에서 500은 샘플 값일 뿐입니다. 사용자 지정 플레이헤드 위치에 다른 값을 사용해야 합니다.
