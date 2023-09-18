---
title: 전역 구성 파일
description: 전역 구성 파일
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 전역 구성 파일{#global-configuration-file}

flashaccess-global.xml 구성 파일에는 라이센스 서버의 모든 테넌트에 적용되는 설정이 포함되어 있습니다. 이 파일은 다음 위치에 있어야 합니다. *LicenseServer.ConfigRoot*. 예제 전역 구성 파일은 configs 디렉토리를 참조하십시오. 전역 구성 파일에는 다음 항목이 포함되어 있습니다.

* 캐싱 — 메모리에 있는 구성 파일의 캐싱을 제어합니다. 캐싱 설정에 대한 자세한 내용은 &quot;구성 파일 업데이트&quot;를 참조하십시오.
* 로깅 — 로깅 수준과 로그 파일이 롤링되는 빈도를 지정합니다.
* HSM 암호 — HSM이 서버 자격 증명을 저장하는 데 사용되는 경우에만 필요합니다.

에 있는 예제 전역 구성 파일의 주석을 참조하십시오 `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` 을 참조하십시오.
