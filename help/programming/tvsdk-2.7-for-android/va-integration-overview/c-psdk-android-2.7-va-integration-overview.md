---
description: TVSDK와 Adobe Analytics을 통합하여 비디오 사용을 추적할 수 있습니다.
title: 비디오 분석
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 개요 {#video-analytics-overview}

TVSDK와 Adobe Analytics을 통합하여 비디오 사용을 추적할 수 있습니다.

TVSDK에서 비디오 추적은 **Adobe Analytics Video Essentials** 서비스를 사용합니다. 이 서비스는 비디오 보기, 비디오 완료, 광고 노출 횟수, 비디오 사용 시간 등과 같은 비디오 참여 지표를 제공합니다. 이 서비스에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

다음 절차에는 플레이어에서 비디오 추적을 활성화하는 단계가 요약되어 있습니다.

1. 다음 비디오 추적 구성 요소를 초기화 및/또는 구성합니다.

   >[!TIP]
   >
   >Android에서 이러한 구성 요소는 TVSDK의 일부입니다.

   * JSON 구성 파일
   * 비디오 분석 메타데이터 개체
   * 전역 메타데이터 개체

1. Adobe Analytics 관리 도구를 사용하여 서버측에서 비디오 분석 보고를 설정합니다.

