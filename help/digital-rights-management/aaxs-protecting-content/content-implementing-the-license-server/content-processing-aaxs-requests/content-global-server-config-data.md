---
seo-title: 전역 서버 구성 데이터
title: 전역 서버 구성 데이터
uuid: f6d6cb01-2645-4cd2-83ec-0272323a67cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 전역 서버 구성 데이터{#global-server-configuration-data}

라이센스 서버에서 사용하는 구성 외에도 `HandlerConfiguration` 클라이언트에 전송하여 라이센스가 적용되는 방식을 제어할 수 있는 구성 정보를 저장합니다. 이 작업은 `ServerConfigData` 클래스를 만들고 전화하여 수행됩니다. `HandlerConfiguration.setServerConfigData()` (이러한 설정은 이 라이선스 서버에서 발급한 라이선스에만 적용됩니다.) 클럭 윈드백 허용치는 클라이언트가 라이센스를 적용하는 방법을 제어하기 위해 라이센스 서버에서 설정할 수 있는 하나의 속성입니다. 기본적으로 사용자는 라이선스를 무효화하지 않고 시스템 시계를 4시간 뒤로 설정할 수 있습니다. 라이선스 서버 운영자가 다른 설정을 사용하려면 `ServerConfigData` 클래스에서 새 값을 설정할 수 있습니다. 이러한 설정의 값을 변경할 때는 반드시 호출함으로써 버전 번호를 증가시켜야 `setVersion()`합니다. 새 값은 클라이언트의 버전이 현재 `ServerConfigData` 버전보다 작은 경우에만 클라이언트에 전송됩니다.
