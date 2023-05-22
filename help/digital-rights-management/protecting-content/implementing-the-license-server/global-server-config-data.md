---
title: 전역 서버 구성 데이터
description: 전역 서버 구성 데이터
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 전역 서버 구성 데이터{#global-server-configuration-data}

라이센스 서버에서 사용하는 구성 외에도 `HandlerConfiguration` 는 라이선스가 적용되는 방식을 제어하기 위해 클라이언트에 보낼 수 있는 구성 정보를 저장합니다. 이 작업은 다음을 생성하여 수행합니다 `ServerConfigData` 클래스 및 호출 `HandlerConfiguration.setServerConfigData()`. 이 설정은 이 라이선스 서버에서 발급한 라이선스에만 적용됩니다.

클럭 윈드백 허용 오차는 클라이언트가 라이선스를 집행하는 방법을 제어하기 위해 라이선스 서버에서 설정할 수 있는 속성 중 하나입니다. 기본적으로 사용자는 라이센스를 무효화하지 않고 기계 시계를 4시간 뒤로 설정할 수 있습니다. 라이센스 서버 운영자가 다른 설정을 사용하려는 경우 새 값을 `ServerConfigData` 클래스. 이러한 설정의 값을 변경할 때는 를 호출하여 버전 번호를 증가시켜야 합니다 `setVersion()`. 클라이언트의 버전이 현재 버전보다 오래된 경우에만 새 값이 클라이언트에 전송됩니다 `ServerConfigData` 버전.
