---
title: 난수 생성
description: 난수 생성
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# 난수 생성{#generating-random-numbers}

충분한 엔트로피가 생성되도록 하기 위해 Linux 서버에서 하드웨어 난수 생성기를 사용할 수 있습니다. 시스템이 충분한 엔트로피를 생성할 수 없는 경우, 무작위의 소스가 필요한 Adobe 액세스 작업은 다음 위치의 데이터를 기다리는 동안 차단됩니다. `/dev/random`.
