---
title: 사용 규칙
description: 사용 규칙
copied-description: true
exl-id: 0f6df09f-47fd-4a05-bcb0-786beaba325a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 사용 규칙{#usage-rules}

Adobe Access Server for Protected Streaming을 사용하면 구성 파일을 통해 서버에 모든 사용 규칙이 지정됩니다. 보호된 콘텐츠에 지정된 모든 사용 규칙은 재정의되므로 콘텐츠 패키징 중 간단한 익명 정책을 사용하는 것이 좋습니다. 구성 가능한 사용 규칙은 테넌트별로 설정할 수 있습니다.

Protected Streaming용 Adobe Access Server은 다음 사용 규칙을 지원합니다.

* 출력 보호
* Adobe® AIR®, SWF, iOS 및 Android 애플리케이션 제한 사항
* DRM 및 런타임 모듈 제한 사항
* 탈옥 탐지 적용(탈옥 탐지를 지원하는 Adobe 액세스 플랫폼에서)
* 라이선스 캐싱은 기본적으로 비활성화되어 있습니다. 라이선스 캐싱은 캐싱 종료 날짜를 지정하거나 캐싱이 허용되는 시간(라이선스 발급 시부터 시작)을 지정하여 활성화할 수 있습니다.
* 다중 재생 권한 - 출력 보호, 응용 프로그램 제한 및 DRM/런타임 제한의 다양한 조합을 지정할 수 있습니다. 예를 들어 출력 보호와 함께 DRM 모듈 제한을 사용하여 각 클라이언트 플랫폼에 대해 서로 다른 출력 보호 요구 사항을 지정할 수 있습니다.

>[!NOTE]
>
>iOS 장치에 대한 원격 키 전달을 지원하려면 패키징 시 사용된 정책에 원격 키 전달이 활성화되어 있어야 합니다. 서버의 테넌트 구성을 통해 이 설정을 수정할 수 없습니다. ***Adobe Primetime은 Adobe 액세스 보호 콘텐츠를 재생할 수 있는 iOS 애플리케이션을 빌드하는 데 필요합니다.***
