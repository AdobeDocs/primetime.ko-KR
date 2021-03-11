---
description: AES-128 암호화 방법은 헤더를 포함한 전체 전송 스트림(TS) 컨테이너를 암호화하는 반면, SAMPLE-AES 암호화는 오디오 및 비디오 데이터의 일부만을 암호화합니다.
title: 샘플 AES 암호화 HLS 스트림
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# 샘플 AES 암호화된 HLS 스트림{#sample-aes-encrypted-hls-streams}

AES-128 암호화 방법은 헤더를 포함한 전체 전송 스트림(TS) 컨테이너를 암호화하는 반면, SAMPLE-AES 암호화는 오디오 및 비디오 데이터의 일부만을 암호화합니다.

암호화된 스트림에서 보호 프로세스가 완료된 보호 블록이 식별됩니다. H.264 비디오 보호 블록은 네트워크 적응 레이어(NAL) 단위의 1 및 5 유형의 본문입니다. 보호된 오디오 블록은 오디오 프레임이고 오디오는 AAC 형식이어야 합니다.

>[!IMPORTANT]
>
>키와 초기화 벡터(IV)가 있어야 합니다. 브라우저 TVSDK는 키와 IV를 사용하여 스트림을 재생하기 전에 해당 스트림의 암호를 해독합니다.

각 보호 블록에는 패딩이 없는 AES-128 CBC(Cipher Block-Chiling) 모드를 사용하여 암호화된 16바이트 블록 정수가 포함되어 있습니다. CBC는 보호되는 각 블록에서 발생하며, 새로 보호된 각 블록이 시작될 때 IV를 원래 값으로 재설정해야 합니다.

다음 코덱이 지원됩니다.

* 비디오의 경우 H.264가 지원됩니다.
* 오디오의 경우 sample-AES는 AAC에서만 지원됩니다.

