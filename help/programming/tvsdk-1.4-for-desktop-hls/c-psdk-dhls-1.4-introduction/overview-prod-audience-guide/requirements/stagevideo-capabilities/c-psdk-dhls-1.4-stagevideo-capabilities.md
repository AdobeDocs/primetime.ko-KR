---
description: GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 비디오를 처리할 수 있습니다. StageVideo의 사용 가능 여부는 Flash Player, 비디오 하드웨어, OS, 드라이버, 브라우저, 네트워크 연결 및 컨텍스트 보기 등 시스템의 여러 부분에 대한 버전 및 기능에 따라 다릅니다.
title: StageVideo 기능 및 제한 사항
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 개요 {#stagevideo-capabilities-and-restrictions-overview}

GPU(하드웨어) 가속을 지원하는 장치에서는 flash.media.StageVideo 객체를 사용하여 장치 하드웨어에서 비디오를 처리할 수 있습니다. StageVideo의 사용 가능 여부는 Flash Player, 비디오 하드웨어, OS, 드라이버, 브라우저, 네트워크 연결 및 컨텍스트 보기 등 시스템의 여러 부분에 대한 버전 및 기능에 따라 다릅니다.

다음 `StageVideo` 클래스를 사용하면 하드웨어 가속을 이용하여 디바이스에 대해 가능한 가장 높은 성능 수준으로 비디오를 표시할 수 있습니다. 의 가용성 및 성능 `StageVideo` 은 다음 요인의 영향을 받습니다.

* **하드웨어 가속** - 하드웨어 가속을 사용할 수 있는 경우 `StageVideo` 는 장치 하드웨어에서 비디오를 처리합니다. 하드웨어 가속을 사용할 수 없는 경우 `StageVideo` 응답은 실행 중인 Flash 버전에 따라 다릅니다.

   * *Flash 15 이상* - 하드웨어 가속을 사용할 수 없는 경우 `StageVideo` 소프트웨어로 돌아가 아무것도 할 필요가 없습니다.

     >[!TIP]
     >
     >하드웨어 가속을 사용할 수 없는 경우 성능이 크게 저하될 수 있습니다.

   * *Flash 14 및 이전* - 하드웨어 가속을 사용할 수 없는 경우 `StageVideo` 를 사용할 수 없게 됩니다. 브라우저 또는 GPU에서 하드웨어 가속을 지원하지 않거나 Flash Player에서 꺼져 있는 작은 구성 집합에서는 TVSDK HLS 스택을 사용한 비디오 표시가 실패합니다. 다음에서 *HDS* 파이프라인에서 전환할 수 있습니다. `StageVideo` CPU에서 비디오를 처리하는 대체 개체(예: Video 개체)로

* **프레젠테이션 컨텍스트** - 전체 화면 보기 중, `StageVideo` 는 항상 사용 가능하며 성능은 장치에서 사용할 수 있는 최대 수준이 됩니다. 전체 화면을 보지 않을 때 비디오 프레젠테이션은 브라우저의 설정 및 기능이 사용되는 브라우저 컨텍스트에 속합니다.

* **wmode** - 브라우저 컨텍스트에서 `wmode` 설정은 성능에 매우 중요합니다. Adobe은 다음을 유지할 것을 권장합니다. `wmode` 을 로 설정 `direct` 을 클릭하여 브라우저 컨텍스트에서 최상의 성능을 보장합니다.

  >[!NOTE]
  >
  >다음을 포함하는 요소의 조합 `wmode`, `StageVideo`및 Flash을 사용하면 하드웨어 실행 속도와 사용 중인 Flash 버전에 따라 기능과 제한 사항이 달라집니다.

   * *Flash 15 이상* - `StageVideo` 은(는) 모든 사용 가능 항목에서 사용할 수 있습니다. `wmode` 설정. 그러나 을 설정하는 경우 `wmode` 이 아닌 다른 설정에 `direct`, 성능이 저하될 것입니다.

   * *Flash 14 및 이전* - 를 설정하는 경우 `wmode` 이 아닌 다른 설정에 `direct`, `StageVideo` 일부 브라우저에서는 를 사용할 수 없습니다.
