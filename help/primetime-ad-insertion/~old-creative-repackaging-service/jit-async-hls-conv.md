---
description: CRS는 JIT(just-in-time) 및 비동기 리패키징과 HLS-to-HLS 변환을 제공합니다. 다시 패키징의 결과는 원래 광고 크리에이티브의 HLS 형식 버전입니다. CRS는 필요한 경우 사용할 CDN(Content Delivery Network) 서버에 HLS 형식 버전을 배치합니다.
title: CRS의 주요 용도
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# CRS의 주요 용도 {#main-uses-of-crs}

CRS는 JIT(just-in-time) 및 비동기 리패키징과 HLS-to-HLS 변환을 제공합니다. 다시 패키징의 결과는 원래 광고 크리에이티브의 HLS 형식 버전입니다. CRS는 필요한 경우 사용할 CDN(Content Delivery Network) 서버에 HLS 형식 버전을 배치합니다.

JIT에서 Adobe Primetime 광고 삽입은 비 HLS 광고 크리에이티브를 처음 접하면 재패키징 프로세스를 시작합니다. 따라서 일반적으로 재패키징 프로세스 중에 광고를 실행할 수 있는 기회가 상실됩니다.

비동기 재패키징에서는 광고 크리에이티브가 필요 전에 코드 변환되고 저장되므로 이러한 손실된 기회를 제거할 수 있습니다.

HLS에서 HLS로 변환할 때 CRS는 HLS 광고 크리에이티브를 적절한 크기의 청크로 재포맷하여 일관된 재생을 보장합니다.

## 적시 재포장 {#section_1BA344F2300B49F291865A7461EDFEAE}

JIT 재패키징의 순서는 다음과 같습니다.

1. 매니페스트 서버가 광고를 가져옵니다.
1. 광고 형식이 HLS이면 매니페스트 서버는 광고를 콘텐츠 스트림에 삽입합니다.
1. 형식이 HLS가 아닌 경우(예: MP4, FLV 또는 WebM) 매니페스트 서버는 CDN 서버에서 코드 변환된 버전을 찾습니다. 찾으면 트랜스코딩된 광고를 콘텐츠 스트림에 삽입합니다.
1. 형식이 HLS가 아니고 CDN 서버에 트랜스코딩된 버전이 없는 경우 매니페스트 서버는 광고를 CRS에 전달하여 광고 크리에이티브를 트랜스코딩하고 나중에 사용할 수 있도록 CDN 서버에 결과를 저장합니다.
1. 매니페스트 서버는 광고 없이 콘텐츠를 반환합니다.

## 비동기 재패키징 {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

에 설명된 API를 사용할 수 있습니다. [API 다시 패키징](../~old-creative-repackaging-service/api-repackage.md) 비 HLS 크리에이티브를 사전 코드 처리하여 노출 손실을 최소화하고 수익성을 극대화합니다.

## HLS-HLS 변환 {#section_877A0E7E8FAF4C2DB086A31C24D53435}

버퍼링 및 지연을 방지하기 위해 클라이언트는 작은 청크로 비디오를 다운로드합니다. 청크 크기가 일관되지 않으면 재생이 경련될 수 있습니다. HLS에서 HLS로 변환하면 데이터 청크가 모두 동일한 기간(예: 6초)이 됩니다.

>[!NOTE]
>
>CRS는 수신하는 HLS 버전에 관계없이 HLS 버전 3을 생성합니다.