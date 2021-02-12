---
title: 라이브/선형 스트림에서 Ad Insertion 사용
description: 라이브/선형 스트림에서 Ad Insertion 사용
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# 라이브/선형 스트림에서 Ad Insertion 사용 {#ad-insertion-live-linear-stream}

Primetime Ad Insertion을 통해 매체사는 실시간/선형 스트림 중에 발생하는 복잡하고 표준 광고 삽입 상황을 처리할 수 있습니다.

## 지원되는 큐 형식 {#cue-formats-supported}

Primetime Ad Insertion은 다음을 포함한 다양한 표준 및 비표준 큐 형식을 지원합니다.

* DPI SCTE-35(SCTE-35 향상된 광고 마커)

* [Adobe 디지털 프로그램 삽입 신호 규격](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 이진 SCTE-35(HLS 및 대시 모두)

* 텍스트 SCTE-35(HLS 및 DASH 모두)

추가 세부 사항 또는 기타 지원되는 큐 형식에 대해서는 Primetime 지원 담당자에게 문의하십시오.

## 부분 광고 나누기 지원 {#partial-ad-break-support}

광고 나누기가 시작된 후 뷰어가 라이브/선형 스트림에 들어가는 경우 부분 광고 나누기를 사용할 수 있습니다.  예를 들어 뷰어가 1:00 마크에 2:00 긴 광고 나누기를 입력하는 경우 부분 광고 나누기 삽입은 남은 시간에 광고가 제공되도록 합니다. 부분 광고 브레이크가 삽입되지 않으면 중단 동안 이 뷰어에 광고가 표시되지 않습니다. 미디어 스트림에 적절한 태그가 있는 경우 Primetime Ad Insertion을 사용하면 기본적으로 부분 광고 나누기를 삽입할 수 있습니다.

## 조기 반환(조기 광고 종료) {#early-return-early-ad-exit}

스포츠 이벤트가 갑자기 행동으로 돌아오는 경우와 같이 라이브/선형 스트림에서 광고 중단에서 일찍 반환해야 할 경우가 있습니다. 각 광고 결정 형식에는 &quot;cue-out&quot;(광고) 또는 &quot;cue-in&quot;(컨텐츠)에 대한 태그가 포함되어 있습니다.  광고 브레이크가 종료되기 전에 &quot;cue-in&quot; 태그가 발견되면 Adobe Primetime Ad Insertion에서 해당 큐-인을 확인합니다.  일찍 반품을 활성화하려면 콘텐츠 패키지로 문의하십시오.
