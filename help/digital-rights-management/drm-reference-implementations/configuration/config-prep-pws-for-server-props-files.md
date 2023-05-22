---
title: 서버 속성 파일에 대한 암호 준비
description: 서버 속성 파일에 대한 암호 준비
copied-description: true
exl-id: b613d43d-17ec-44e9-bd14-81f9bb9a7f62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 서버 속성 파일에 대한 암호 준비{#prepare-passwords-for-the-server-properties-files}

참조 구현은 다음을 제공합니다 `ScrambleUtil.class`: 자격 증명 암호의 보안을 보장하는 클래스입니다.

이 도구를 사용하여 암호를 다음에 포함하기 전에 암호화하십시오. [!DNL flashaccess-refimpl.properties] 파일.

도구를 실행하려면 Ant 스크립트나 Java를 사용할 수 있습니다.

유틸리티는 암호화된 암호를 생성합니다. 이 암호는 [!DNL flashaccess-refimpl.properties] 파일.

>[!NOTE]
>
>다음으로 인코딩된 암호 `ScrambleUtil.class` 참조 구현과 함께 제공된 는 Primetime DRM Server for Protected Streaming에서 작동하지 않습니다.
