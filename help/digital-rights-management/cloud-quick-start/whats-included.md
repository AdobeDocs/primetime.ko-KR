---
description: Adobe은 자체 Primetime DRM License Server를 개발 및 유지 관리하지 않으려는 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 이 서비스를 활용하면 고객은 DRM 라이선스 발급을 둘러싼 운영 및 개발 복잡성을 줄일 수 있다. Primetime Cloud DRM은 iOS, Android, 데스크톱 및 Xbox360과 같은 Primetime 브라우저 TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 Adobe에서 호스팅 및 유지 관리되며 24/7 가동 시간이 있습니다.
title: 배경
exl-id: bb5ad080-5b1d-43a6-8d0e-9b5735c82d96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 배경 {#background}

Adobe은 자체 Primetime DRM License Server를 개발 및 유지 관리하지 않으려는 Adobe Primetime DRM 고객에게 클라우드 DRM 서비스를 제공합니다. 이 서비스를 활용하면 고객은 DRM 라이선스 발급을 둘러싼 운영 및 개발 복잡성을 줄일 수 있다. Primetime Cloud DRM은 iOS, Android, 데스크톱 및 Xbox360과 같은 Primetime 브라우저 TVSDK 지원 비디오 애플리케이션을 실행할 수 있는 모든 디바이스에 DRM 라이선스를 발급할 수 있습니다. 이 DRM 서비스는 Adobe에서 호스팅 및 유지 관리되며 24/7 가동 시간이 있습니다.

>[!NOTE]
>
>Adobe Primetime DRM은 이전에 Adobe 액세스라고 하였으며, 그 이전에는 Flash Access 입니다.

## Primetime Cloud DRM에 포함된 기능 {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* 사용자 지정 인증/자격 모듈 및 콘텐츠에 대한 사용자 지정 인증 참여 방법에 대한 지침입니다. 자세한 설명서는 [!DNL Custom Authentication Entitlement] 디렉토리.
* Cloud DRM 관련 라이선스 서버 인증서( [!DNL .pem/.cer/.der])

* Cloud DRM 관련 라이선스 서버 전송 인증서( [!DNL .pem/.cer/.der])

* Primetime Java Offline Package
* 패키지용 샘플 DRM 정책

   * **policy_24hr** - 디스크에 24시간 동안 캐시된 라이센스 24시간 후에는 콘텐츠를 볼 수 있는 새 라이선스를 취득해야 합니다. 이 키트의 다른 모든 정책에도 24시간 라이센스 캐싱이 있습니다.
   * **policy_ios_remotekeyserver** - iOS 장치에서 DRM 라이선스는 Cloud DRM에서 획득됩니다. 또한 클라이언트는 클라우드 DRM에서 모든 AES 암호 해독 키를 획득합니다. 탈옥 iOS 장치에서는 재생이 허용되지 않습니다.

   * **policy_ios_localkeyserver** - iOS 장치에서 DRM 라이선스는 Cloud DRM에서 획득됩니다. 또한 클라이언트는 클라우드 DRM 대신 로컬 HTTP 서버에서 모든 HLS AES 암호 해독 키를 획득합니다. 탈옥 iOS 장치에서는 재생이 허용되지 않습니다.

   * **policy_adobePass** - 먼저 클라이언트를 (이전의 Adobe Pass)로 인증해야 합니다. 그렇지 않으면 라이센스가 거부됩니다.

* 추가 DRM 정책을 생성하는 Adobe 정책 관리자 도구
* 패키징에 사용할 샘플 비디오 콘텐츠
