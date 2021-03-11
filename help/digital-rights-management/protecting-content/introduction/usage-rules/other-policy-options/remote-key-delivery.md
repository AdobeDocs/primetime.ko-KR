---
title: 원격 및 로컬 iOS 키 제공
description: 원격 및 로컬 iOS 키 제공
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# 원격 및 로컬 iOS 키 배달 {#remote-and-local-ios-key-delivery}

Adobe Primetime은 iOS 클라이언트에 키 제공을 위한 다음 옵션을 지원합니다.

* **원격**  - HLS(HTTP Live Streaming) 사양에 지정된 대로 수행합니다.M3U8 매니페스트는 스트림에서 다음과 같은 암호화된 세그먼트를 해독하는 데 사용할 AES 키가 포함된 HTTPS 경로를 지정합니다. Primetime DRM 정책에 `Remote`을(를) 지정하는 경우 클라이언트 장치가 원격 HTTPS 서버에 연결하여 AES 키를 받아야 합니다.

* **로컬**  - AES 키 `Local` 에 대한 인터넷/네트워크에 연결하는 대신 Primetime DRM에서 지정한 경우 로컬 HTTPS 서버가 iOS 애플리케이션에 포함되고 이를 통해 모든 AES 키 요청을 관리합니다. 포함된 HTTPS 서버는 P 응용 프로그램에서 자동으로 설정 및 구성됩니다. 애플리케이션 개발자는 개입할 필요가 없습니다.

원격 키 전달은 콘텐츠를 패키지화하는 데 사용되는 Primetime DRM 정책을 통해 활성화됩니다. 이 설정을 변경하려면 콘텐트를 다시 패키지해야 합니다. 원격 키 제공을 활성화하는 경우 iOS 클라이언트의 키 요청을 관리할 수 있는 Primetime DRM 키 서버를 배포해야 합니다. 그러나 다른 플랫폼의 클라이언트에 대한 워크플로우는 변경되지 않습니다.

>[!NOTE]
>
>키 배달 선택은 iOS 클라이언트에만 영향을 줍니다. 데스크톱(Flash Player)의 Android 및 Primetime 등 HLS 콘텐츠를 사용하는 다른 모든 장치는 `Remote`이(가) 지정되었더라도 항상 `Local` 키 제공을 사용합니다.

