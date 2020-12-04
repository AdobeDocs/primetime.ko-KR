---
description: GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 비디오를 처리할 수 있습니다. StageVideo의 사용 가능 여부는 Flash Player, 비디오 하드웨어, OS, 드라이버, 브라우저, 네트워크 연결, 보기 컨텍스트 등 시스템 여러 부분의 버전과 기능에 따라 다릅니다.
seo-description: GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 비디오를 처리할 수 있습니다. StageVideo의 사용 가능 여부는 Flash Player, 비디오 하드웨어, OS, 드라이버, 브라우저, 네트워크 연결, 보기 컨텍스트 등 시스템 여러 부분의 버전과 기능에 따라 다릅니다.
seo-title: 스테이지 비디오 기능 및 제한 사항
title: 스테이지 비디오 기능 및 제한 사항
uuid: 7556f30b-4b9f-4258-beb6-2a4ce8f05d1a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 개요 {#stagevideo-capabilities-and-restrictions-overview}

GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 비디오를 처리할 수 있습니다. StageVideo의 사용 가능 여부는 Flash Player, 비디오 하드웨어, OS, 드라이버, 브라우저, 네트워크 연결, 보기 컨텍스트 등 시스템 여러 부분의 버전과 기능에 따라 다릅니다.

`StageVideo` 클래스를 사용하면 하드웨어 가속을 활용하여 장치에 대해 가능한 최고 성능 수준에서 비디오를 표시할 수 있습니다. `StageVideo`의 가용성 및 성능은 다음 요인에 의해 영향을 받습니다.

* **하드웨어 가속**  - 하드웨어 가속을 사용할 수  `StageVideo` 있으면 장치 하드웨어에서 비디오를 처리합니다. 하드웨어 가속을 사용할 수 없는 경우 `StageVideo`은 실행 중인 Flash 버전에 따라 달라집니다.

   * *Flash 15 이상*  - 하드웨어 가속을 사용할 수 없는 경우 소프트웨어로  `StageVideo` 돌아가고 아무것도 할 필요가 없습니다.

      >[!TIP]
      >
      >하드웨어 가속을 사용할 수 없는 경우 성능이 크게 저하될 수 있습니다.

   * *Flash 14 및 이전*  버전 - 하드웨어 가속을 사용할 수 없을 때 사용할 수  `StageVideo` 없게 됩니다. 브라우저 또는 GPU에서 하드웨어 가속을 지원하지 않거나 Flash Player에서 꺼진 작은 구성에서는 TVSDK HLS 스택을 사용한 비디오 디스플레이가 실패합니다. *HDS* 파이프라인에서 CPU에서 비디오를 처리하는 `StageVideo`에서 대체(예: 비디오 개체)로 전환할 수 있습니다.

* **프레젠테이션 컨텍스트**  - 전체 화면을 보는 동안 항상 사용  `StageVideo` 가능하며 성능은 장치에서 사용할 수 있는 최대 수준에 있습니다. 전체 화면을 볼 수 없는 경우 비디오 프레젠테이션은 브라우저의 설정 및 기능이 사용되는 브라우저의 상황에 해당됩니다.

* **wmode**  - 브라우저 컨텍스트에서  `wmode` 설정은 성능에 중요합니다. Adobe은 브라우저 컨텍스트에서 최상의 성능을 얻으려면 `wmode`을 `direct`로 설정하는 것이 좋습니다.

   >[!NOTE]
   >
   >하드웨어 실행 속도 및 사용 중인 Flash 버전에 따라 `wmode`, `StageVideo` 및 Flash을 포함하는 요소의 조합으로 다양한 기능과 제한이 발생합니다.

   * *Flash 15 이상*  - 사용  `StageVideo` 가능한 모든  `wmode` 설정에서 사용할 수 있습니다. 그러나 `wmode`을(를) `direct` 이외의 설정으로 설정하면 성능이 저하됩니다.

   * *Flash 14 및 이전*  버전 - 다른 설정 `wmode`  `direct`으로 설정하면 일부 브라우저 `StageVideo` 에서 사용할 수없습니다.

