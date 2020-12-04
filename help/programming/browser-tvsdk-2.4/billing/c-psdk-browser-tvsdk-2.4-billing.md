---
description: 실제 사용에 상관없이 고정 요금 대신 사용한 만큼만 지불하려는 고객을 수용하기 위해 Adobe은 사용 지표를 수집하고 이러한 지표를 사용하여 고객에게 청구할 비용을 결정합니다.
seo-description: 실제 사용에 상관없이 고정 요금 대신 사용한 만큼만 지불하려는 고객을 수용하기 위해 Adobe은 사용 지표를 수집하고 이러한 지표를 사용하여 고객에게 청구할 비용을 결정합니다.
seo-title: 청구 지표
title: 청구 지표
uuid: e09b77b3-89d3-44d6-be4e-e1612fbf89fc
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 개요 {#billing-metrics-overview}

실제 사용에 상관없이 고정 요금 대신 사용한 만큼만 지불하려는 고객을 수용하기 위해 Adobe은 사용 지표를 수집하고 이러한 지표를 사용하여 고객에게 청구할 비용을 결정합니다.

플레이어가 스트림 시작 이벤트를 생성할 때마다 Browser TVSDK는 주기적으로 HTTP 메시지를 Adobe 결제 시스템으로 보내기 시작합니다. 청구 가능한 기간이라고 하는 기간은 표준 VOD, 프로 VOD(미드롤 광고 활성화) 및 라이브 컨텐츠에 대해 다를 수 있습니다. 각 컨텐츠 유형의 기본 기간은 30분이지만 Adobe과의 계약에 따라 실제 값이 결정됩니다.

메시지에는 다음 정보가 포함되어 있습니다.

* 컨텐츠 유형(라이브, 선형 또는 VOD)
* 콘텐트 URL
* 광고 활성화 여부
* 중간 롤 광고 활성화 여부(VOD만 해당)
* 스트림이 DRM으로 보호되는지 여부
* 브라우저 TVSDK 버전 및 플랫폼

Adobe은 이 배열을 미리 구성하지만, 배열을 변경하려면 Adobe 활성 담당자에게 문의하십시오.

Browser TVSDK가 Adobe으로 전송하는 통계를 모니터링하려면 Adobe 활성 담당자의 URL을 입수하고, 데이터를 보려면 Charles와 같은 네트워크 캡처 도구를 사용하십시오.
