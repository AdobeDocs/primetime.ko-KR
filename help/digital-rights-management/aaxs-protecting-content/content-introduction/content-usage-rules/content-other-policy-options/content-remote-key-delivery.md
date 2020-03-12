---
seo-title: 원격 및 로컬 iOS 키 전달
title: 원격 및 로컬 iOS 키 전달
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 원격 및 로컬 iOS 키 전달{#remote-and-local-ios-key-delivery}

Adobe Primetime은 iOS 클라이언트에 키 제공을 위한 두 가지 옵션을 지원합니다.

* 원격 - HLS 사양에 정확히 지정된 대로 M3U8 매니페스트는 스트림에서 다음 암호화된 세그먼트를 해독하는 데 사용할 AES 키가 포함된 HTTPS 경로를 지정합니다. &quot;원격&quot;을 지정하면 클라이언트 장치가 원격 HTTPS 서버에 연결하여 AES 키를 가져옵니다.
* 로컬 - &quot;로컬&quot;을 지정하면 AES 키에 대한 인터넷/네트워크를 통해 연결하는 대신 로컬 HTTPS 서버가 모든 AES 키 요청을 처리하는 iOS 애플리케이션에 포함됩니다. 포함된 HTTPS 서버는 Primetime 애플리케이션에 자동으로 설정되고 구성됩니다. 애플리케이션 개발자는 개입할 필요가 없습니다.

원격 키 배달은 컨텐츠를 패키지하는 데 사용되는 정책을 통해 활성화됩니다(이 설정을 변경하려면 컨텐츠를 다시 패키지해야 함). 원격 키 배달이 활성화되면 iOS 클라이언트의 주요 요청을 처리하기 위해 Adobe Access Key Server를 배포해야 하지만 다른 플랫폼의 클라이언트에 대한 워크플로우는 변경되지 않습니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>키 배달 선택은 iOS 클라이언트에만 영향을 줍니다. HLS 컨텐츠를 사용하는 다른 모든 장치는 &quot;원격&quot;이 지정된 경우에도 항상 &quot;로컬&quot; 키 제공을 사용합니다.

자세한 내용은 Adobe Access *키 서버 사용을 참조하십시오*.
