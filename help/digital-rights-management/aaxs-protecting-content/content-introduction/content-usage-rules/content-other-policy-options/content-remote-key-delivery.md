---
title: 원격 및 로컬 iOS 키 전달
description: 원격 및 로컬 iOS 키 전달
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 원격 및 로컬 iOS 키 전달{#remote-and-local-ios-key-delivery}

Adobe Primetime은 iOS 클라이언트에 키 전달을 위한 두 가지 옵션을 지원합니다.

* 원격 - HLS 사양에 지정된 대로 M3U8 매니페스트는 스트림에서 다음 암호화된 세그먼트를 해독하는 데 사용해야 하는 AES 키가 포함된 HTTPS 경로를 지정합니다. &quot;Remote&quot;를 지정하면 클라이언트 장치가 원격 HTTPS 서버에 연결하여 AES 키를 가져옵니다.
* 로컬 - &quot;로컬&quot;를 지정하면 AES 키를 인터넷/네트워크를 통해 전달하는 대신 로컬 HTTPS 서버가 iOS 애플리케이션에 포함되어 모든 AES 키 요청을 처리합니다. 임베드된 HTTPS 서버는 Primetime 애플리케이션에서 자동으로 설정되고 구성됩니다. 응용 프로그램 개발자는 개입할 필요가 없습니다.

원격 키 전달은 콘텐츠를 패키지하는 데 사용되는 정책을 통해 활성화됩니다(이 설정을 변경하면 콘텐츠를 다시 패키징해야 함). 원격 키 전달을 사용하는 경우, iOS 클라이언트의 키 요청을 처리하기 위해 Adobe 액세스 키 서버를 배포해야 하지만, 다른 플랫폼의 클라이언트에 대해서는 워크플로를 변경하지 않습니다.

>[!NOTE]
>
>키 전달 선택은 iOS 클라이언트에만 영향을 줍니다. HLS 콘텐츠를 사용하는 다른 모든 장치는 &quot;원격&quot;이 지정된 경우에도 항상 &quot;로컬&quot; 키 전달을 사용합니다.

자세한 내용은 *Adobe 액세스 키 서버 사용*.
