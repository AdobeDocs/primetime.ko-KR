---
description: CRS는 적시(JIT) 및 비동기 재패키징 및 HLS-HLS 간 변환을 제공합니다. 재패키징 결과는 원본 광고 크리에이티브의 HLS 형식 버전입니다. CRS는 HLS 형식 버전을 필요할 때 사용할 수 있도록 CDN(Content Delivery Network) 서버에 배치합니다.
seo-description: CRS는 적시(JIT) 및 비동기 재패키징 및 HLS-HLS 간 변환을 제공합니다. 재패키징 결과는 원본 광고 크리에이티브의 HLS 형식 버전입니다. CRS는 HLS 형식 버전을 필요할 때 사용할 수 있도록 CDN(Content Delivery Network) 서버에 배치합니다.
seo-title: CRS의 기본 사용
title: CRS의 기본 사용
uuid: df2caa67-bc94-4146-9b93-14edc060c3d5
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# CRS {#main-uses-of-crs}의 기본 사용

CRS는 적시(JIT) 및 비동기 재패키징 및 HLS-HLS 간 변환을 제공합니다. 재패키징 결과는 원본 광고 크리에이티브의 HLS 형식 버전입니다. CRS는 HLS 형식 버전을 필요할 때 사용할 수 있도록 CDN(Content Delivery Network) 서버에 배치합니다.

JIT에서 Adobe Primetime 광고 삽입은 HLS가 아닌 광고 크리에이티브가 발견되면 재패키징 프로세스를 시작합니다. 일반적으로 재패키징 프로세스 중에 광고를 실행할 수 있는 기회를 잃게 됩니다.

비동기식 재패키징에서 광고 크리에이티브는 필요하기 전에 코드 변환되어 저장되므로 손실되는 기회를 없앨 수 있습니다.

HLS에서 HLS로 변환하는 경우 CRS는 HLS 광고를 적절한 크기의 청크로 다시 포맷하여 일관된 재생을 보장합니다.

## 적시 재패키징 {#section_1BA344F2300B49F291865A7461EDFEAE}

JIT 재패키징의 시퀀스는 다음과 같습니다.

1. 매니페스트 서버가 광고를 가져옵니다.
1. 광고 형식이 HLS이면 매니페스트 서버가 광고를 콘텐츠 스트림에 삽입합니다.
1. 형식이 HLS(예: MP4, FLV 또는 WebM)가 아닌 경우 매니페스트 서버는 CDN 서버에서 코드 변환된 버전을 찾습니다. 이를 찾으면 코드 변환된 광고를 컨텐츠 스트림에 삽입합니다.
1. 형식이 HLS가 아니며 CDN 서버에 트랜스코딩된 버전이 없는 경우 매니페스트 서버는 광고를 CRS로 전달하여 광고 크리에이티브를 트랜스코딩하고 결과를 나중에 사용하도록 CDN 서버에 저장합니다.
1. 매니페스트 서버는 광고 없이 콘텐츠를 반환합니다.

## 비동기 재패키징 {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

[API 재패키징](../~old-creative-repackaging-service/api-repackage.md)에 설명된 API를 사용하여 HLS가 아닌 크리에이티브 코드를 미리 변환하여 노출 손실을 최소화하고 가치 창출을 극대화할 수 있습니다.

## HLS-HLS 변환 {#section_877A0E7E8FAF4C2DB086A31C24D53435}

버퍼링 및 지연을 방지하기 위해 클라이언트는 작은 청크로 비디오를 다운로드합니다. 청크 크기가 일관되지 않은 경우 재생이 불안정할 수 있습니다. HLS에서 HLS로 변환하면 데이터 청크가 모두 동일한 기간(예: 6초)이 됩니다.

>[!NOTE]
>
>CRS는 수신하는 HLS 버전에 관계없이 HLS 버전 3을 생성합니다.