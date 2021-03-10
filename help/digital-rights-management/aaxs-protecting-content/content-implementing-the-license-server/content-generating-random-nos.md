---
title: 난수 생성
description: 난수 생성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# 난수 생성 중{#generating-random-numbers}

하드웨어 무작위 번호 생성기는 충분한 엔트로피가 생성되도록 Linux 서버에서 사용할 수 있습니다. 컴퓨터가 충분한 엔트로피를 생성할 수 없는 경우 랜덤의 소스가 필요한 Adobe 액세스 작업은 `/dev/random`의 데이터를 기다리는 동안 차단됩니다.
