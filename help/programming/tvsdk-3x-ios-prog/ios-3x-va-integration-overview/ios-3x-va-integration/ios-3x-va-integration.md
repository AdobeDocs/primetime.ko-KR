---
description: TVSDK를 Adobe Analytics과 통합하여 비디오 사용을 추적할 수 있습니다.
title: 비디오 분석 통합
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 비디오 분석 통합 {#video-analytics-integration}

TVSDK를 Adobe Analytics과 통합하여 비디오 사용을 추적할 수 있습니다.

TVSDK의 비디오 추적은 **Adobe Analytics Video Essentials** 비디오 보기 횟수, 비디오 전체 보기 횟수, 광고 노출 횟수, 비디오 체류 시간 등과 같은 비디오 참여 지표를 제공하는 서비스입니다. 이 서비스에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

다음 절차에서는 플레이어에서 비디오 추적을 활성화하는 단계를 요약합니다.

1. 다음 비디오 추적 구성 요소를 초기화 및/또는 구성합니다.

   iOS에서 이러한 구성 요소는 TVSDK의 일부입니다.

   * JSON 구성 파일
   * 비디오 분석 메타데이터 개체
   * 전역 메타데이터 개체
   * Video Analytics 추적기 개체

1. Adobe Analytics 관리 도구를 사용하여 서버측에서 비디오 분석 보고를 설정합니다.
