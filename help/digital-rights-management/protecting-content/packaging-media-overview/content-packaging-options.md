---
title: 패키징 옵션
description: 패키징 옵션
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# 패키징 옵션{#packaging-options}

컨텐츠를 패키지화하는 데 사용할 수 있는 다양한 옵션이 있습니다. `DRMParameters` 인터페이스에서 옵션을 지정할 수 있으며 인터페이스를 사용할 수 있는 클래스를 구현할 수 있습니다. 이러한 클래스를 사용하여 서명 및 키 매개 변수를 설정할 수 있을 뿐만 아니라 오디오 내용, 비디오 내용 또는 스크립트 데이터를 암호화할 것인지를 지정할 수 있습니다. 이러한 구현이 참조 구현에서 구현되는 방식을 보려면 *Adobe Primetime DRM 참조 구현 사용*&#x200B;에서 설명한 Media Packager 명령줄 옵션에 대한 설명을 참조하십시오. 이러한 옵션은 Java API를 기반으로 하므로 프로그래밍 방식으로 사용할 수 있습니다.

패키지 옵션은 다음과 같습니다.

* 암호화 옵션(오디오, 비디오, 부분 암호화).
* 라이센스 서버로 전송되는 모든 요청에 대해 클라이언트가 기본 URL로 사용하는 라이센스 서버 URL
* 라이선스 서버 전송 인증서
* CEK를 암호화하는 데 사용되는 라이센스 서버 인증서
* 메타데이터 서명을 위한 Packager 자격 증명

