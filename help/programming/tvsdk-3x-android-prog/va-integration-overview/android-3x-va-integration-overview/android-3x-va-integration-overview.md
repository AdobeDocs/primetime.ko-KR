---
description: TVSDK와 Adobe Analytics를 통합하여 비디오 사용을 추적할 수 있습니다.
seo-description: TVSDK와 Adobe Analytics를 통합하여 비디오 사용을 추적할 수 있습니다.
seo-title: Adobe Analytics와 TVSDK 통합
title: Adobe Analytics와 TVSDK 통합
uuid: 4d498d35-ec8e-40fc-8272-1637ef942bb0
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Adobe Analytics와 TVSDK 통합 {#integrating-tvsdk-with-adobe-analytics}

TVSDK와 Adobe Analytics를 통합하여 비디오 사용을 추적할 수 있습니다.

TVSDK에서 비디오 추적은 **Adobe Analytics Video Essentials** 서비스를 사용하며, 비디오 보기 횟수, 비디오 완료, 광고 노출 횟수, 비디오 사용 시간 등과 같은 비디오 참여 지표를 제공합니다. 이 서비스에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

다음 절차에는 플레이어에서 비디오 추적을 활성화하는 단계가 요약되어 있습니다.

1. 다음 비디오 추적 구성 요소를 초기화 및/또는 구성합니다.

   >[!TIP]
   >
   >Android에서 이러한 구성 요소는 TVSDK의 일부입니다.

   * JSON 구성 파일
   * 비디오 분석 메타데이터 개체
   * 전역 메타데이터 개체

1. Adobe Analytics 관리 도구를 사용하여 서버측에서 비디오 분석 보고를 설정합니다.