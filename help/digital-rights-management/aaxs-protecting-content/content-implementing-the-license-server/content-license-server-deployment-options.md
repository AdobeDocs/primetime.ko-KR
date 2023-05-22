---
title: 라이선스 서버 배포 옵션
description: 라이선스 서버 배포 옵션
copied-description: true
exl-id: c7422a8f-2cd1-4ace-8706-eb3e5a55eac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 라이선스 서버 배포 옵션{#license-server-deployment-options}

라이센스 서버는 다음 옵션 중 하나를 사용하여 배포할 수 있습니다.

* **Adobe Access Server for Protected Streaming** — 이 라이센스 서버는 스트리밍에 최적화되어 있습니다. 예를 들어 Adobe 액세스를 사용하여 Adobe HTTP Dynamic Streaming에 대한 서버를 설정할 수 있습니다. 이 서버는 구성이 거의 필요 없이 쉽게 배포할 수 있으며 여러 테넌트를 지원하며 높은 수준의 확장성을 얻을 수 있습니다. 하지만 이 구현은 스트리밍에 최적화되었기 때문에 전체 Adobe 액세스 기능을 지원하지 않습니다. 예를 들어 사용자 이름/암호 인증, 도메인 및 라이선스 체인은 지원되지 않습니다. 이 서버에서 발급한 라이선스의 사용 규칙은 패키징 시 사용된 정책을 재지정하는 서버 구성 파일을 통해 제어됩니다. 다음을 참조하십시오. *Adobe Access Server for Protected Streaming 안내서* 이 서버에서 지원하는 사용 규칙에 대한 자세한 내용을 보려면 여기를 클릭하십시오.
* **참조 구현 라이선스 서버** — 이 설정을 사용자 정의 서버 구현의 시작점으로 사용합니다. 다음은 Adobe Access SDK에서 API를 사용하여 모든 유형의 요청을 처리하는 방법과 데이터베이스에서 지원하는 사용자 지정 비즈니스 논리를 구현하는 방법을 보여 주는 소스 코드를 포함한 예제 라이선스 서버 구현입니다. 이 서버에서 발급한 라이선스의 사용 규칙은 패키징 시 콘텐츠와 관련된 정책을 통해 제어됩니다.
* **사용자 지정 서버 구현** — SDK를 사용하여 고유한 라이센스 서버를 구현할 수도 있습니다. 이 장의 정보는 라이선스 서버를 구현하는 데 사용되는 API에 대해 설명합니다.
