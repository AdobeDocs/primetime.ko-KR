---
description: 'null'
seo-description: 'null'
seo-title: 서버 속성 파일에 대한 암호 준비
title: 서버 속성 파일에 대한 암호 준비
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 서버 속성 파일에 대한 암호 준비{#prepare-passwords-for-the-server-properties-files}

참조 구현에서 제공하는 `ScrambleUtil.class`클래스로, 자격 증명의 암호 보안을 보장합니다.

이 도구를 사용하여 암호를 [!DNL flashaccess-refimpl.properties] 파일에 포함하기 전에 암호화합니다.

도구를 실행하려면 Ant 스크립트나 Java를 사용할 수 있습니다.

이 유틸리티는 암호화된 암호를 생성하므로 [!DNL flashaccess-refimpl.properties] 파일에 복사해야 합니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>참조 구현과 함께 `ScrambleUtil.class` 제공된 암호로 인코딩된 암호는 보호된 스트리밍을 위한 Primetime DRM Server에서 작동하지 않습니다.
