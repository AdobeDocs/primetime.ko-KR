---
description: 이 섹션에서는 다양한 버전의 Flash Player 및 TVSDK에서 사용할 수 있는 기능에 대해 설명합니다.
seo-description: 이 섹션에서는 다양한 버전의 Flash Player 및 TVSDK에서 사용할 수 있는 기능에 대해 설명합니다.
seo-title: RBOP 클라이언트 지원
title: RBOP 클라이언트 지원
uuid: d1d0f788-7bc1-488c-807e-be47f83725e9
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# RBOP 클라이언트 지원 {#rbop-client-support}

이 섹션에서는 다양한 버전의 Flash Player 및 TVSDK에서 사용할 수 있는 기능에 대해 설명합니다.

**오류 디스패치**  - 재생되는 컨텐츠의 해상도가 DRM 정책에 정의된 장치 구성에 대해 허용되는 해상도를 초과하는 경우 아래 나열된 TVSDK 플랫폼이 DRM 런타임 오류를 전달합니다.

* Flash Player 버전 18 - 20
* Android - 버전
* iOS - 버전

>[!NOTE]
>
>* 모든 Flash 및 모바일 플랫폼은 오류 디스패치를 지원하지만 위에 나열된 TVSDK 클라이언트만 RBOP 관련 오류를 처리합니다.
>* RBOP 관련 [DRM 클라이언트 오류](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371** - 라이센스의 출력 보호 제한 사항을 기반으로 한 잘못된 형식의 해상도.
   >    * **3372** - 내용 해상도가 출력 보호 제약 조건에 지정된 최대 해상도보다 큽니다. (다른 장치에 사용할 내용을 삽입하려고 하면 이러한 문제가 발생할 수 있습니다.)
   >    * **3373** - 컨텐츠의 해상도가 현재 활성 출력 보호 제약 조건에 의해 지정된 해상도보다 큽니다. (즉, 다운그레이드해야 합니다.)

>



**자동 다운스케일링**  - 축소 작업에 사용되는 기술은 플랫폼 및 Flash Player 버전에 따라 다릅니다.

* Flash Player 버전 21:자동 다운크기 조정(지능적인 비트 전송률 전환)을 통해 RBOP 지원
* Windows 기반의 Firefox 버전 38 이상(액세스 CDM 포함):Adobe은 더 높은 비트 전송률 스트림을 더 낮은 스트림으로 자동 다운그레이드합니다(다운그레이드된 스트림이 아니라).

>[!NOTE]
>
>이러한 플랫폼은 자동으로 비디오를 축소하고 DRM 정책에 지정된 해상도보다 작거나 같은 해상도로 컨텐츠를 표시합니다. 이 기능을 사용하면 DRM 정책 제한 사항을 충족하는 사용 가능한 스트림이 있을 경우 항상 콘텐츠가 클라이언트에 재생됩니다.

**기존 출력 보호**  - 버전 18 이전의 Flash Player을 사용하는 클라이언트는 기존 OP 제한만을 처리할 수 있습니다. Flash Player 버전 18 이상이 있는 클라이언트는 레거시 또는 RBOP 제한을 처리할 수 있습니다. RBOP 제한을 설정하는 경우 이전 클라이언트에 대한 기존 OP 제한도 설정해야 합니다. RBOP를 지원하는 클라이언트의 경우, RBOP 제한은 기존 OP 제한을 뛰어넘습니다.
