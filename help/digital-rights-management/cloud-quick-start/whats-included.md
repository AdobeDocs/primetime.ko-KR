---
description: Adobe은 고유한 Primetime DRM 라이선스 서버를 개발하고 유지 관리하지 않으려는 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 고객은 이 서비스를 활용하여 DRM 라이선스 발급과 관련된 운영 및 개발 복잡성을 줄일 수 있습니다. Primetime Cloud DRM은 iOS, Android, 데스크탑 및 Xbox 360과 같은 Primetime Browser TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 24시간 연중무휴 가동되므로 Adobe에 의해 호스팅되고 유지 관리됩니다.
seo-description: Adobe은 고유한 Primetime DRM 라이선스 서버를 개발하고 유지 관리하지 않으려는 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 고객은 이 서비스를 활용하여 DRM 라이선스 발급과 관련된 운영 및 개발 복잡성을 줄일 수 있습니다. Primetime Cloud DRM은 iOS, Android, 데스크탑 및 Xbox 360과 같은 Primetime Browser TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 24시간 연중무휴 가동되므로 Adobe에 의해 호스팅되고 유지 관리됩니다.
seo-title: 배경
title: 배경
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# 배경 {#background}

Adobe은 고유한 Primetime DRM 라이선스 서버를 개발하고 유지 관리하지 않으려는 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 고객은 이 서비스를 활용하여 DRM 라이선스 발급과 관련된 운영 및 개발 복잡성을 줄일 수 있습니다. Primetime Cloud DRM은 iOS, Android, 데스크탑 및 Xbox 360과 같은 Primetime Browser TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 24시간 연중무휴 가동되므로 Adobe에 의해 호스팅되고 유지 관리됩니다.

>[!NOTE]
>
>Adobe Primetime DRM은 이전에 Adobe 액세스라고 불렸으며 그 이전에는 Flash Access으로 불렸습니다.

## Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}에 포함된 제품

* 사용자 정의 인증/권한 부여 모듈 및 컨텐츠에 대한 사용자 정의 인증 참여 방법에 대한 지침 자세한 내용은 [!DNL Custom Authentication Entitlement] 디렉토리를 참조하십시오.
* 클라우드 DRM별 라이선스 서버 인증서( [!DNL .pem/.cer/.der])

* 클라우드 DRM별 라이선스 서버 전송 인증서( [!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* 패키징을 위한 샘플 DRM 정책

   * **policy_24hr** - 24시간 동안 디스크의 라이센스 캐시 24시간 후 컨텐츠를 보려면 새로운 라이센스를 취득해야 합니다. 이 키트의 다른 모든 정책에는 24시간 라이선스 캐싱도 포함되어 있습니다.
   * **policy_ios_remotekeyserver**  - iOS 디바이스에서 DRM 라이선스는 Cloud DRM에서 획득됩니다. 또한 클라이언트는 클라우드 DRM에서 모든 AES 암호 해독 키를 획득합니다. 중복을 입은 iOS 장치에서 재생을 허용하지 않습니다.

   * **policy_ios_localkeyserver**  - iOS 디바이스에서 DRM 라이선스는 Cloud DRM에서 취득됩니다. 또한 클라이언트는 클라우드 DRM 대신 로컬 HTTP 서버에서 모든 HLS AES 암호 해독 키를 획득합니다. 중복을 입은 iOS 장치에서 재생을 허용하지 않습니다.

   * **policy_adobePass**  - 클라이언트가 먼저 인증 대상(이전의 Adobe Pass)을 해야 하거나 라이센스가 거부됩니다.

* Adobe 정책 관리자 도구를 사용하여 추가 DRM 정책 만들기
* 패키징에 사용할 샘플 비디오 컨텐츠

