---
seo-title: Primetime DRM 키 서버 사용 요구 사항
title: Primetime DRM 키 서버 사용 요구 사항
uuid: 769f9e10-7a3e-4a38-b30d-18181b666bb4
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 소개 {#introduction}

Primetime DRM Key Server는 원격 iOS 및/또는 Xbox 360 키 제공을 위한 멀티 테넌트 키 서버입니다. iOS에 대한 정책에서 원격 키 전달을 사용하는 경우 iOS 클라이언트에서 콘텐츠를 재생하려면 Primetime DRM 키 서버를 배포해야 합니다. Primetime DRM 키 서버는 Xbox 360에 항상 필요합니다.

## Primetime DRM 키 서버 사용 요구 사항 {#requirements-for-using-primetime-drm-key-server}

Primetime DRM 키 서버 사용을 위한 최소 요구 사항은 다음과 같습니다.

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 이상 (Windows 64비트에서 HSM을 사용하려면 JRE 8이 필요합니다.)

   >[!NOTE]
   >
   >64비트 PKCS11이 이제 OpenJDK 8에서 지원됩니다.https://openjdk.java.net/jeps/131 [](https://openjdk.java.net/jeps/131)및 Oracle JDK:https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559 [](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Adobe에서 발행한 자격 증명
* Microsoft에서 발행한 자격 증명(Xbox 360 클라이언트용)