---
description: TVSDK를 Adobe Analytics과 통합하여 비디오 사용을 추적할 수 있습니다.
title: 비디오 분석
exl-id: 02303511-2713-4974-ada7-6f50fc500325
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 비디오 분석{#video-analytics}

TVSDK를 Adobe Analytics과 통합하여 비디오 사용을 추적할 수 있습니다.

TVSDK의 비디오 추적은 **Adobe Analytics Video Essentials** 비디오 보기 횟수, 비디오 전체 보기 횟수, 광고 노출 횟수, 비디오 체류 시간 등과 같은 비디오 참여 지표를 제공하는 서비스입니다. 이 서비스에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

다음 절차에서는 플레이어에서 비디오 추적을 활성화하는 단계를 요약합니다.

1. 다음 비디오 추적 구성 요소를 초기화 및/또는 구성합니다.

   * **AppMeasurement 라이브러리** - 하위 수준 데이터 수집 핵심 논리를 포함합니다. 여기서 비디오 하트비트 데이터가 축적되고 네트워크를 통해 전송됩니다.
   * **비디오 하트비트 라이브러리** - 비디오 하트비트 데이터 수집 코어 논리를 포함합니다. 비디오 하트비트 라이브러리는 의 하위 집합에 액세스합니다 `AppMeasurement` 라이브러리 API.

      >[!TIP]
      >
      >앱은 비디오 하트비트 코드와 직접 상호 작용하지 않습니다. 대신 앱은 TVSDK API를 사용하여 플레이어의 비디오 추적 기능을 구성합니다.

   * **VisitorID 라이브러리** - 비디오 플레이어를 호스팅하는 웹 페이지 방문자를 고유하게 식별합니다.
   >[!IMPORTANT]
   >
   >TVSDK 기본 제공 비디오 추적 기능은 올바르게 구성된 `AppMeasurement` 인스턴스. 추적 요소는 다음과 같이 가정합니다. `AppMeasurement` 비디오 추적을 구성하고 활성화하기 전에 라이브러리가 이미 인스턴스화되고 구성되었습니다. TVSDK 비디오 추적 기능은 의 완전히 기능하고 올바르게 구성된 인스턴스가 있는지 여부에 따라 다릅니다. `AppMeasurement` 라이브러리입니다.

1. Adobe Analytics 관리 도구를 사용하여 서버측에서 비디오 분석 보고를 설정합니다.
