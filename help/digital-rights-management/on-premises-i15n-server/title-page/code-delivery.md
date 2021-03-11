---
title: 코드 전달/패키지 내용
description: 코드 전달/패키지 내용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 코드 배달 / 패키지 내용{#code-delivery-package-contents}

Adobe Primetime DRM 온 프레미스 개인 설정 서버 패키지에는 다음 내용이 포함되어 있습니다.

* [!DNL flashaccess.war] - 개인화 서버
* [!DNL flashaccess-kgs.war] - 선택적인 키 생성 서버
* [!DNL /shared] - 다음을 포함:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - 샘플 속성 파일

* [!DNL thirdparty/] - 기본 라이브러리로 Crypto-J 지원 포함:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - 서버 자격 증명 암호를 암호화하는 유틸리티
* [!DNL ROOT] -  [!DNL crossdomain.xml] 파일 포함

* ECI 캐시 파일 - 사전 다운로드
* [!DNL addIndivCert.py] - 온-프레미스 개인화를 지원하기 위해 라이센스 서버의 신뢰 루트를 업데이트하는 스크립트
* [!DNL CreateMetadata.jar] - 온-프레미스 DRM 메타데이터 만들기 유틸리티
* [!DNL client_sample/] - 클라이언트 코드 조각이 있는 폴더
* 릴리스 노트 - 문서에 추가된 마지막 순간에 대한 추가 사항

