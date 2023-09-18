---
title: 원격 및 로컬 iOS 키 전달
description: 원격 및 로컬 iOS 키 전달
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 원격 및 로컬 iOS 키 전달 {#remote-and-local-ios-key-delivery}

Adobe Primetime은 iOS 클라이언트에 키를 전달하기 위해 다음 옵션을 지원합니다.

* **원격** - HLS(HTTP Live Streaming) 사양에 지정된 대로 수행합니다. M3U8 매니페스트는 스트림에서 다음 암호화된 세그먼트를 해독하는 데 사용해야 하는 AES 키가 포함된 HTTPS 경로를 지정합니다. 을 지정하는 경우 `Remote` Primetime DRM 정책에서 클라이언트 장치는 원격 HTTPS 서버에 연결하여 AES 키를 받아야 합니다.

* **로컬** - 를 지정할 때 `Local` Primetime DRM에서는 AES 키를 위해 인터넷/네트워크에 연결하는 대신 로컬 HTTPS 서버가 iOS 애플리케이션에 임베드되어 모든 AES 키 요청을 관리합니다. 임베드된 HTTPS 서버는 P 애플리케이션에서 자동으로 설정 및 구성됩니다. 응용 프로그램 개발자는 개입할 필요가 없습니다.

원격 키 전달은 콘텐츠를 패키지하는 데 사용되는 Primetime DRM 정책을 통해 활성화됩니다. 이 설정을 변경하려면 콘텐츠를 다시 패키징해야 합니다. 원격 키 전달을 사용하는 경우 iOS 클라이언트의 키 요청을 관리할 수 있는 Primetime DRM 키 서버를 배포해야 합니다. 그러나 다른 플랫폼의 클라이언트에 대한 워크플로는 변경되지 않습니다.

>[!NOTE]
>
>키 전달 선택은 iOS 클라이언트에만 영향을 줍니다. Android 및 Primetime on Desktop(Flash Player)과 같이 HLS 콘텐츠를 사용하는 다른 모든 장치는 항상 를 사용합니다 `Local` 키 전달, 다음과 같은 경우에도 `Remote` 이(가) 지정되었습니다.
