---
title: 라이브/선형 스트림에서 Ad Insertion 사용
description: 라이브/선형 스트림에서 Ad Insertion 사용
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 라이브/선형 스트림에 Ad Insertion 사용 {#ad-insertion-live-linear-stream}

Primetime Ad Insertion을 통해 발행자는 실시간/선형 스트림 중에 발생하는 표준 및 복잡한 광고 삽입 상황을 처리할 수 있습니다.

## 지원되는 큐 형식 {#cue-formats-supported}

Primetime Ad Insertion은 다음을 비롯한 다양한 표준 및 비표준 큐 포맷을 지원합니다.

* DPI SCTE-35(SCTE-35 향상된 광고 마커)

* [Adobe 디지털 프로그램 삽입 신호규격](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 바이너리 SCTE-35

자세한 내용이나 기타 지원되는 큐 포맷은 Primetime 지원 담당자에게 문의하십시오.

## 부분 광고 중단 지원 {#partial-ad-break-support}

광고 나누기가 시작된 후 뷰어가 라이브/선형 스트림에 들어가는 경우 부분 광고 나누기를 사용할 수 있습니다.  예를 들어 뷰어가 1:00 마크에 2:00 긴 광고 나누기를 입력하는 경우 부분 광고 중단 삽입으로 광고가 나머지 시간에 제공될 것입니다. 부분 광고 중단 삽입 없이는 휴식 시간 동안 이 뷰어에 광고가 표시되지 않습니다. Primetime Ad Insertion을 사용하면 미디어 스트림에 적절한 태그가 있는 경우 기본적으로 부분 광고 나누기를 삽입할 수 있습니다.

## 조기 재방문(조기 광고 종료) {#early-return-early-ad-exit}

스포츠 이벤트가 갑자기 행동으로 돌아가는 경우와 같이 라이브/선형 스트림의 광고 중단에서 일찍 반환해야 할 경우가 있습니다. 각 광고 결정 형식에는 &quot;큐 아웃&quot;(광고) 또는 &quot;큐 인&quot;(컨텐츠)에 대한 태그가 포함되어 있습니다. 광고 중단 전에 &quot;cue-in&quot; 태그가 발견되면 Adobe Primetime Ad Insertion이 해당 큐 인을 확인합니다. 조기 반품을 활성화하려면 컨텐츠 패키저에 문의하십시오.
