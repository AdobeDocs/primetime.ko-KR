---
seo-title: 라이선스 서버 배포 옵션
title: 라이선스 서버 배포 옵션
uuid: 732b948f-8037-423e-9f85-770d6316cbae
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 라이선스 서버 배포 옵션{#license-server-deployment-options}

다음 옵션 중 하나를 사용하여 라이센스 서버를 배포할 수 있습니다.

* 보호된 스트리밍을 위한 Adobe Primetime DRM 서버—이 라이센스 서버는 스트리밍을 위해 최적화되어 있습니다. 예를 들어 Primetime DRM을 사용하여 Adobe HTTP Dynamic Streaming용 서버를 설정할 수 있습니다. 이 서버는 구성이 거의 필요하지 않고 쉽게 배포할 수 있으며 여러 세입자를 지원합니다. 높은 수준의 확장성을 얻을 수 있습니다. 이 구현은 스트리밍에 최적화되어 있으므로 Primetime DRM의 모든 기능을 지원하지 않습니다. 예를 들어, 사용자 이름/암호 인증, 도메인 및 라이선스 체인은 지원되지 않습니다. 이 서버에서 발행한 라이센스의 사용 규칙은 서버 구성 파일을 통해 제어되며, 이는 패키징 시 사용된 정책을 덮어씁니다.

   라이센스 서버에서 지원하는 사용 규칙에 대한 자세한 내용은 *Adobe Primetime DRM Server for Protected Streaming 안내서*&#x200B;를 참조하십시오.
* 구현 라이센스 서버 참조 - 이 설정을 사용하여 서버 구현을 사용자 정의할 수 있습니다. 소스 코드를 비롯한 라이선스 서버 구현의 예입니다. 이 예제에서는 Primetime DRM SDK에서 API를 사용하여 모든 유형의 요청을 관리하고 데이터베이스를 기반으로 맞춤형 비즈니스 로직을 구현하는 방법을 보여 줍니다. 이 서버에서 발행한 라이선스의 사용 규칙은 패키징 시 컨텐츠와 관련된 정책을 통해 제어됩니다.
* 사용자 지정 서버 구현—SDK를 사용하여 자체 라이센스 서버를 구현할 수도 있습니다. 이 정보는 API를 사용하여 라이센스 서버를 구현하는 방법을 설명합니다.

