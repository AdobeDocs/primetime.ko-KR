---
title: 키 저장
description: 키 저장
copied-description: true
exl-id: 922e1e2c-8d4a-41f6-8f4d-7db0522f39d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 키 저장{#store-keys}

Adobe은 컨텐츠 게시자가 서명 및 암호화를 위한 암호화 개인 키를 안전하고 변조가 불가능한 하드웨어 장치에 저장할 것을 권장합니다. 소프트웨어에 저장된 키는 하드웨어에 저장된 키보다 쉽게 손상될 수 있습니다. 예를 들어 소프트웨어 키가 유출되면 일반적으로 키가 들어 있는 키나 파일이 복사되기 때문에 침해를 감지하기 어렵습니다. 하드웨어에 저장된 키는 감지되지 않은 손상에 덜 취약합니다.

하드웨어 보안 모듈(HSM)은 암호화 키를 저장하고 보호하는 전용 하드웨어 장치입니다. 자세한 내용은 *자격 증명 저장* 위치: *컨텐츠 보호를 위해 Adobe Primetime DRM SDK 사용*.
