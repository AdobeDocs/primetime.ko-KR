---
description: flashaccess-global.xml 구성 파일에는 라이센스 서버의 모든 테넌트에 적용되는 설정이 포함되어 있습니다.
title: 전역 구성 파일
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 전역 구성 파일{#global-configuration-file}

flashaccess-global.xml 구성 파일에는 라이센스 서버의 모든 테넌트에 적용되는 설정이 포함되어 있습니다.

에 구성 파일을 배치해야 합니다. [!DNL LicenseServer.ConfigRoot] 디렉토리.

다음을 참조하십시오. [!DNL configs] 디렉토리(전역 구성 파일 예제).

전역 구성 파일에는 다음이 포함되어 있습니다.

* 캐싱 — 메모리에 있는 구성 파일의 캐싱을 제어합니다.

  다음을 참조하십시오 *구성 파일 업데이트 중* 캐싱 설정에 대한 자세한 정보.
* 로깅 — 로깅 수준과 로그 파일이 롤링되는 빈도를 지정합니다.
* HSM 암호 — HSM이 서버 자격 증명을 저장하는 데 사용되는 경우에만 필요합니다.

Primetime DRM에 있는 예제 글로벌 구성 파일의 주석을 참조하십시오 `<DVD>`자세한 내용은 \Adobe Primetime DRM Server for Protected Streaming\configs를 참조하십시오.
