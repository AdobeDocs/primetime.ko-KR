---
title: 라이브/선형 스트림에서 Ad Insertion 사용
description: 라이브/선형 스트림에서 Ad Insertion 사용
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 라이브/선형 스트림에서 Ad Insertion 사용 {#ad-insertion-live-linear-stream}

Primetime Ad Insertion은 게시자에게 라이브/선형 스트림 중에 발생하는 표준 및 복잡한 광고 삽입 상황을 처리할 수 있는 기능을 제공합니다.

## 지원되는 큐 형식 {#cue-formats-supported}

Primetime Ad Insertion은 다음을 포함한 광범위한 표준 및 비표준 큐 형식을 지원합니다.

* DPI SCTE-35(SCTE-35 향상된 광고 마커)

* [Adobe 디지털 프로그램 삽입 시그널링 사양](assets/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 이진 SCTE-35(HLS 및 DASH 모두)

* 텍스트 SCTE-35(HLS 및 대시 모두)

자세한 내용이나 기타 지원되는 큐 형식은 Primetime 지원 담당자에게 문의하십시오.

## 부분 광고 브레이크 지원 {#partial-ad-break-support}

부분 광고 브레이크는 광고 브레이크가 시작된 후 뷰어가 라이브/선형 스트림에 들어가는 상황에서 사용할 수 있습니다.  예를 들어, 뷰어가 1시 표시에 2시 길이의 광고 브레이크를 입력하면 나머지 시간에 광고가 게재되도록 부분 광고 브레이크 삽입이 이루어집니다. 부분 광고 브레이크를 삽입하지 않으면 브레이크 중에 이 뷰어에 광고가 제공되지 않습니다. 미디어 스트림에 적절한 태그가 있는 경우 Primetime Ad Insertion은 기본적으로 부분 광고 브레이크 삽입을 활성화합니다.

## 조기 복귀(조기 광고 종료) {#early-return-early-ad-exit}

스포츠 이벤트가 갑자기 동작으로 돌아오는 경우와 같이 라이브/선형 스트림에서 광고 브레이크에서 조기에 반환해야 하는 경우가 있습니다. 각 광고 결정 형식에는 &quot;cue-out&quot;(ads) 또는 &quot;cue-in&quot;(content)에 대한 태그가 포함되어 있습니다.  광고 브레이크가 끝나기 전에 &quot;큐 인&quot; 태그가 발견되면 Adobe Primetime Ad Insertion이 큐 인을 처리합니다.  조기 반환을 활성화하려면 콘텐츠 포장기에 문의하십시오.
