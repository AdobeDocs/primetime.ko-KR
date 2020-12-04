---
description: 'null'
seo-description: 'null'
seo-title: 서버 속성 파일에 대한 암호 준비
title: 서버 속성 파일에 대한 암호 준비
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 서버 속성 파일에 대한 암호 준비{#prepare-passwords-for-the-server-properties-files}

참조 구현에서는 자격 증명 암호의 보안을 보장하는 클래스인 `ScrambleUtil.class`을 제공합니다.

이 도구를 사용하여 암호를 [!DNL flashaccess-refimpl.properties] 파일에 포함하기 전에 암호화합니다.

도구를 실행하려면 Ant 스크립트나 Java를 사용할 수 있습니다.

이 유틸리티는 암호화된 암호를 생성하며 이 암호를 [!DNL flashaccess-refimpl.properties] 파일에 복사해야 합니다.

>[!NOTE]
>
>참조 구현과 함께 제공된 `ScrambleUtil.class`으로 인코딩된 암호는 보호된 스트리밍을 위한 Primetime DRM Server에서 작동하지 않습니다.
