---
title: 코드 변환 및 표준화
description: 코드 변환 및 표준화
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 코드 변환 및 표준화 {#transcoding-and-normalization}

Primetime Ad Insertion은 다음과 일치시키려고 시도하여 콘텐츠 및 광고 전반에 걸쳐 일관된 보기 환경을 보장하려고 합니다.

1. 소스 스트림 코덱 및 비트율, 코드 변환 시 항상 가장 높은 품질/비트율 크리에이티브 선택

1. 소스 스트림 조각 크기(HLS/#EXT-X-TARGETDURATION)

1. 코드 변환에 선호하는 크리에이티브 형식

1. 모든 광고 크리에이티브에서 일관된 dB 수준을 보장하기 위한 오디오 자동 레벨링.

>[!NOTE]
>
>Primetime Ad Insertion just-in time 트랜스코딩에서 생성된 HLS 에셋은 콘텐츠에 정의된 HLS 버전에 관계없이 버전 3의 HLS 에셋을 생성합니다.
