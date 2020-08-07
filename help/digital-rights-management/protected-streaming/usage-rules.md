---
description: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버를 사용하면 구성 파일이 있는 서버의 모든 사용 규칙을 지정할 수 있습니다.
seo-description: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버를 사용하면 구성 파일이 있는 서버의 모든 사용 규칙을 지정할 수 있습니다.
seo-title: 사용 규칙 정보
title: 사용 규칙 정보
uuid: 4a794712-db58-43f5-b867-8871e58e12ae
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# 사용 규칙 정보{#about-usage-rules}

보호된 스트리밍을 위한 Adobe Primetime DRM 서버를 사용하면 구성 파일이 있는 서버의 모든 사용 규칙을 지정할 수 있습니다.

보호된 콘텐츠에 대한 DRM 정책에 지정된 사용 규칙은 재정의됩니다. 따라서 Adobe은 컨텐츠 패키징 중에 익명 DRM 정책을 사용하는 것이 좋습니다. 구성할 수 있는 모든 사용 규칙은 테넌트 단위로 구성할 수 있습니다.

보호된 스트리밍을 위한 Primetime DRM 서버는 다음 사용 규칙을 지원합니다.

* 출력 보호
* Adobe® AIR®, SWF, iOS 및 Android 애플리케이션 제한 사항
* DRM 및 런타임 모듈 제한 사항
* Primetime DRM 플랫폼에 대한 탈옥의 감지
* 기본적으로 라이선스 캐싱은 비활성화됩니다. 캐싱 종료 날짜 또는 시간 캐싱을 지정하여 활성화할 수 있는 라이센스 캐싱라이센스가 발급되면 시작됩니다.
* 출력 보호, 응용 프로그램 제한 및 DRM/런타임 제한 사항의 서로 다른 조합을 지정할 수 있는 다중 재생 권한. 예를 들어 출력 보호에서 DRM 모듈 제한을 사용하여 각 클라이언트 플랫폼에 대해 서로 다른 출력 보호 요구 사항을 지정할 수 있습니다.

>[!NOTE]
>
>iOS 장치에 대한 원격 키 제공을 지원하려는 경우 패키징 시에 적용되는 DRM 정책에 원격 키 게재를 활성화해야 합니다. 이 설정은 서버의 테넌트 구성을 통해 수정할 수 없습니다.

