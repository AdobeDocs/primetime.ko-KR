---
description: Browser TVSDK와 Adobe Analytics을 통합하여 비디오 사용을 추적할 수 있습니다.
title: 비디오 분석
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# 비디오 분석{#video-analytics}

Browser TVSDK와 Adobe Analytics을 통합하여 비디오 사용을 추적할 수 있습니다.

브라우저 TVSDK의 비디오 추적은 **Adobe Analytics Video Essentials** 서비스를 사용하며, 이 서비스는 비디오 보기, 비디오 완료, 광고 노출 횟수, 비디오 사용 시간 등과 같은 비디오 참여 지표를 제공합니다. 이 서비스에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

다음 절차에는 플레이어에서 비디오 추적을 활성화하는 단계가 요약되어 있습니다.

1. 다음 비디오 추적 구성 요소를 초기화 및/또는 구성합니다.

   * **AppMeasurement 라이브러리**  - 하위 수준 데이터 수집 핵심 논리를 포함합니다. 비디오 하트비트 데이터가 누적되어 네트워크를 통해 전송되는 곳입니다.
   * **비디오 하트비트 라이브러리**  - 비디오 하트비트 데이터 수집 핵심 논리를 포함합니다. 비디오 하트비트 라이브러리는 AppMeasurement 라이브러리 API의 하위 세트에 액세스합니다.

      >[!TIP]
      >
      >앱이 비디오 하트비트 코드와 직접적으로 상호 작용하지 않습니다. 대신 앱은 브라우저 TVSDK API를 사용하여 플레이어의 비디오 추적 기능을 구성합니다.

   * **VisitorID 라이브러리**  - 비디오 플레이어를 호스팅하는 웹 페이지의 방문자를 고유하게 식별합니다.
   >[!IMPORTANT]
   >
   >브라우저 TVSDK 내장 비디오 추적 기능은 올바르게 구성된 AppMeasurement 인스턴스에 따라 달라집니다. 추적 요소는 비디오 추적을 구성하고 활성화하기 전에 AppMeasurement 라이브러리가 이미 인스턴스화되고 구성되어 있다고 가정합니다. 브라우저 TVSDK 비디오 추적 기능은 AppMeasurement 라이브러리의 올바르게 기능적이고 구성된 인스턴스가 존재하는지에 따라 달라집니다.

1. Adobe Analytics 관리 도구를 사용하여 서버측에서 비디오 분석 보고를 설정합니다.