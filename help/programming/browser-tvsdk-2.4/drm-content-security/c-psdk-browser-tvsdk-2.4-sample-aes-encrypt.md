---
description: AES-128 암호화 방법은 헤더를 포함하는 전체 전송 스트림(TS) 컨테이너를 암호화하지만, SAMPLE-AES 암호화는 오디오와 비디오 데이터의 일부만 암호화합니다.
title: 샘플 AES 암호화 HLS 스트림
exl-id: 04bda50f-5ca4-4a00-bb5a-97259a2cb005
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# 샘플 AES 암호화 HLS 스트림{#sample-aes-encrypted-hls-streams}

AES-128 암호화 방법은 헤더를 포함하는 전체 전송 스트림(TS) 컨테이너를 암호화하지만, SAMPLE-AES 암호화는 오디오와 비디오 데이터의 일부만 암호화합니다.

암호화된 스트림에서는 보호 프로세스가 완료된 보호 블록이 식별됩니다. H.264 비디오 보호 블록은 NAL(Network Adaptation Layer) 유닛의 타입 1 및 타입 5의 바디이다. 오디오의 보호된 블록은 오디오 프레임이며 오디오는 AAC 형식이어야 합니다.

>[!IMPORTANT]
>
>키와 초기화 벡터(IV)가 있어야 합니다. 브라우저 TVSDK는 재생하기 전에 키와 IV를 사용하여 스트림을 해독합니다.

각 보호 블록에는 패딩이 없는 AES-128 CBC(암호화 블록 체인) 모드를 사용하여 암호화된 16바이트 블록의 정수가 포함되어 있습니다. CBC는 각각의 보호 블록에서 발생하고, 각각의 새로운 보호 블록의 시작 시에 IV는 그의 원래의 값으로 재설정되어야 한다.

지원되는 코덱은 다음과 같습니다.

* 비디오의 경우 H.264가 지원됩니다.
* 오디오의 경우 sample-AES는 AAC에서만 지원됩니다.
