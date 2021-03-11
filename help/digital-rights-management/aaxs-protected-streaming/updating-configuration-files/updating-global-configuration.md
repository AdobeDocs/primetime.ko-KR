---
title: 전역 구성 파일 업데이트
description: 전역 구성 파일 업데이트
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# 전역 구성 파일 업데이트 중{#updating-the-global-configuration-file}

[!DNL flashaccess-global.xml]의 HSM 암호는 언제든지 수정할 수 있으며, 변경 사항은 서버에서 다음에 구성 파일을 다시 로드할 때 적용됩니다. 하지만 &quot;로깅&quot; 및 &quot;캐싱&quot; 요소에 대한 변경 내용은 다시 로드되지 않습니다.이러한 요소를 변경하면 서버를 다시 시작해야 합니다.
