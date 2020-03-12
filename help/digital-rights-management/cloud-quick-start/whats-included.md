---
description: Adobe는 고유한 Primetime DRM 라이선스 서버를 개발 및 유지 관리하고 싶지 않은 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 고객은 이 서비스를 활용하여 DRM 라이선스 발급 시 운영 및 개발 복잡성을 줄일 수 있습니다. Primetime Cloud DRM은 iOS, Android, Desktop 및 Xbox360과 같은 Primetime Browser TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 24시간 연중무휴 Adobe에서 호스팅 및 유지 관리합니다.
seo-description: Adobe는 고유한 Primetime DRM 라이선스 서버를 개발 및 유지 관리하고 싶지 않은 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 고객은 이 서비스를 활용하여 DRM 라이선스 발급 시 운영 및 개발 복잡성을 줄일 수 있습니다. Primetime Cloud DRM은 iOS, Android, Desktop 및 Xbox360과 같은 Primetime Browser TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 24시간 연중무휴 Adobe에서 호스팅 및 유지 관리합니다.
seo-title: 배경
title: 배경
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 배경 {#background}

Adobe는 고유한 Primetime DRM 라이선스 서버를 개발 및 유지 관리하고 싶지 않은 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 고객은 이 서비스를 활용하여 DRM 라이선스 발급 시 운영 및 개발 복잡성을 줄일 수 있습니다. Primetime Cloud DRM은 iOS, Android, Desktop 및 Xbox360과 같은 Primetime Browser TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 24시간 연중무휴 Adobe에서 호스팅 및 유지 관리합니다.

>[!NOTE]
>
>Adobe Primetime DRM의 이전 명칭은 Adobe Access였으며 그 이전에는 Flash Access였습니다.

## Primetime Cloud DRM에 포함된 제품 {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* 사용자 정의 인증/권한 부여 모듈과 콘텐츠에 대한 사용자 정의 인증 참여 방법에 대한 지침 자세한 내용은 [!DNL Custom Authentication Entitlement] 디렉토리를 참조하십시오.
* 클라우드 DRM 관련 라이선스 서버 인증서( [!DNL .pem/.cer/.der])

* 클라우드 DRM 관련 라이선스 서버 전송 인증서( [!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* 패키징을 위한 샘플 DRM 정책

   * **policy_24hr** - 24시간 동안 디스크의 라이선스 캐시 24시간 이후에는 컨텐츠를 보려면 새로운 라이센스를 취득해야 합니다. 이 키트의 다른 모든 정책에도 24시간 라이선스 캐싱이 있습니다.
   * **policy_ios_remotekeyserver** - iOS 장치에서 DRM 라이선스는 Cloud DRM에서 취득됩니다. 또한 클라이언트는 클라우드 DRM에서 모든 AES 암호 해독 키를 획득합니다. 가드레싱된 iOS 장치에서 재생이 허용되지 않습니다.

   * **policy_ios_localkeyserver** - iOS 장치에서 DRM 라이선스는 Cloud DRM에서 취득됩니다. 또한 클라이언트는 클라우드 DRM 대신 로컬 HTTP 서버에서 모든 HLS AES 암호 해독 키를 획득합니다. 가드레싱된 iOS 장치에서 재생이 허용되지 않습니다.

   * **policy_adobePass** - 클라이언트가 먼저 인증 대상(이전 Adobe Pass)을 해야 하거나 라이센스가 거부됩니다.

* Adobe Policy Manager 툴을 사용하여 추가 DRM 정책 만들기
* 패키징에 사용할 샘플 비디오 컨텐츠

