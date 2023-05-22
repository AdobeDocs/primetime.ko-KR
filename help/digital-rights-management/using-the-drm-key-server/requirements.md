---
title: Primetime DRM 키 서버 사용을 위한 요구 사항
description: Primetime DRM 키 서버 사용을 위한 요구 사항
copied-description: true
exl-id: a5c0db05-15a1-45b0-abb9-11f857f5e34c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 소개 {#introduction}

Primetime DRM 키 서버는 원격 iOS 및/또는 Xbox 360 키 전달을 위한 다중 테넌트 키 서버입니다. iOS에 대한 정책에서 원격 키 전달이 활성화된 경우 iOS 클라이언트에서 컨텐츠 재생을 활성화하려면 Primetime DRM 키 서버를 배포해야 합니다. Xbox 360에는 Primetime DRM 키 서버가 항상 필요합니다.

## Primetime DRM 키 서버 사용을 위한 요구 사항 {#requirements-for-using-primetime-drm-key-server}

Primetime DRM 키 서버를 사용하기 위한 최소 요구 사항은 다음과 같습니다.

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 나중에 Windows 64비트에서 HSM을 사용하려면 JRE 8이 필요합니다.

   >[!NOTE]
   >
   >64비트 PKCS11은 이제 OpenJDK 8에서 지원됩니다. [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)및 Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Adobe에서 발급한 자격 증명
* Microsoft에서 발급한 자격 증명(Xbox 360 클라이언트용)
