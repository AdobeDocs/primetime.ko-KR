---
title: 일반 워크플로우
description: 일반 워크플로우
copied-description: true
exl-id: c2020b48-7e97-4df5-a453-7b76e2e1d458
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 일반 워크플로우{#typical-workflow}

명령줄 도구와 라이선스 서버를 모두 제공하는 일반적인 Primetime DRM 참조 구현 워크플로입니다.

1. 정책 명령줄 도구를 사용하여 DRM 정책을 생성합니다.
1. Packager 명령줄 도구를 사용하여 콘텐츠를 암호화합니다.
1. 참조 구현 라이선스 서버 배포.
1. 웹 서버에 비디오 플레이어를 업로드합니다.
1. 업로드된 비디오 플레이어를 사용하여 라이선스를 획득하고 암호화된 콘텐츠를 재생합니다.

이 일반적인 워크플로에서는 명령줄 도구와 라이선스 서버를 모두 사용하므로 계속하기 전에 두 구성 요소를 모두 설치하고 구성할 수 있습니다.
