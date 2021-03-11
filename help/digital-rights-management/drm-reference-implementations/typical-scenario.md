---
title: 일반적인 워크플로우
description: 일반적인 워크플로우
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 일반적인 워크플로{#typical-workflow}

명령줄 툴과 라이선스 서버를 모두 제공하는 일반적인 Primetime DRM 참조 구현 워크플로우입니다.

1. 정책 명령줄 도구를 사용하여 DRM 정책을 만듭니다.
1. Packager 명령줄 도구를 사용하여 내용을 암호화합니다.
1. 참조 구현 라이선스 서버를 배포합니다.
1. 웹 서버에 비디오 플레이어를 업로드합니다.
1. 업로드된 비디오 플레이어를 사용하여 라이선스를 입수하고 암호화된 내용을 재생합니다.

이 일반적인 워크플로우에서는 명령줄 도구와 라이센스 서버를 모두 사용하므로 계속하기 전에 이러한 구성 요소를 모두 설치하고 구성합니다.
