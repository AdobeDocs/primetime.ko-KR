---
seo-title: 장치 그룹 도메인 등록
title: 장치 그룹 도메인 등록
uuid: 221bf6c3-0568-443d-b761-64715a57ada6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 장치 그룹 도메인 등록{#device-group-domain-registration}

특정 디바이스에 라이선스를 바인딩하는 대신 Primetime DRM 3.0 이상에서는 디바이스 도메인에 대한 바인딩 라이선스를 지원합니다.

여러 장치가 도메인에 가입하고 도메인 토큰을 수신할 수 있습니다. 도메인의 한 장치가 라이센스를 취득한 후 라이센스를 도메인의 다른 장치로 전송할 수 있으며 라이센스 서버에서 직접 라이센스를 취득하지 않고도 해당 장치가 컨텐트를 재생할 수 있습니다.

도메인 바인딩된 라이선스를 지원하려는 경우 Primetime DRM 정책은 클라이언트가 등록해야 하는 도메인 서버를 지정해야 합니다. 또한 Primetime DRM 정책은 익명 액세스가 활성화되었는지 또는 서버가 사용자 이름/암호 또는 사용자 정의 인증을 필요로 하는지 여부와 관계없이 도메인 서버에 대한 인증 요구 사항을 지정해야 합니다.

도메인 등록 및 도메인 기반의 라이선스는 Primetime DRM 클라이언트 버전 3.0 이상에서 지원됩니다. Flash Player의 이전 클라이언트 또는 Adobe Primetime 3.0 클라이언트가 도메인 등록을 지원하는 콘텐츠에 대한 라이선스를 요청하는 경우 라이선스 서버는 특정 디바이스에 대한 바인딩을 지원하기 위해 대체 Primetime DRM 정책을 사용하는 라이선스를 발급할 수 있습니다.
