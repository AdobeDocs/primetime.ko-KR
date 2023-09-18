---
description: 이 섹션에서는 다양한 버전의 Flash Player 및 TVSDK에서 사용할 수 있는 기능에 대해 설명합니다.
title: RBOP 클라이언트 지원
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# RBOP 클라이언트 지원 {#rbop-client-support}

이 섹션에서는 다양한 버전의 Flash Player 및 TVSDK에서 사용할 수 있는 기능에 대해 설명합니다.

**오류 발송** - 아래 나열된 TVSDK 플랫폼은 재생 중인 콘텐츠 해상도가 DRM 정책에 정의된 장치 구성에 허용된 해상도를 초과할 때 DRM 런타임 오류를 발송합니다.

* Flash Player 버전 18 - 20
* Android - 버전
* iOS - 버전

>[!NOTE]
>
>* 모든 Flash 및 모바일 플랫폼은 오류 디스패치를 지원하지만, 위에 나열된 TVSDK 클라이언트만 RBOP 관련 오류를 처리합니다.
>* RBOP 관련 [DRM 클라이언트 오류](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
>    * **3371** - 라이선스의 출력 보호 제한에 따라 잘못된 해결 방법.
>    * **3372** - 콘텐츠 해상도가 출력 보호 제한에 지정된 최대 해상도보다 큽니다. (이 문제는 누군가가 다른 장치에 해당하는 콘텐츠를 주입하려고 할 때 발생할 수 있습니다.)
>    * **3373** - 콘텐츠 해상도가 현재 활성 출력 보호 제한에 지정된 해상도보다 큽니다. (즉, 다운그레이드해야 합니다.)
>

**자동 다운스케일링** - 다운스케일에 사용되는 기술은 플랫폼 및 Flash Player 버전에 따라 다릅니다.

* Flash Player 버전 21: 자동 다운스케일링으로 RBOP 지원(지능형 비트율 스위칭)
* Windows의 Firefox 버전 38 이상(Access CDM 사용): Adobe은 자동으로 더 높은 비트율 스트림을 더 낮은 비트율 스트림으로 다운그레이드합니다(더 낮은 등급의 스트림 다운로드와 반대).

>[!NOTE]
>
>이러한 플랫폼은 자동으로 비디오를 축소하고 DRM 정책에서 지정한 해상도보다 작거나 같은 해상도로 콘텐츠를 표시합니다. 이 기능을 사용하면 DRM 정책 제한을 충족하는 사용 가능한 스트림이 있는 한 콘텐츠는 항상 클라이언트에 재생됩니다.

**기존 출력 보호** - 버전 18 이전의 Flash Player을 사용하는 클라이언트는 이전 OP 제한만 처리할 수 있습니다. Flash Player 버전 18 이상의 클라이언트는 기존 또는 RBOP 제한을 처리할 수 있습니다. RBOP 제한을 설정하는 경우 이전 클라이언트에 대한 이전 OP 제한도 설정해야 합니다. RBOP를 지원하는 클라이언트의 경우, RBOP 제한이 기존 OP 제한을 무시합니다.
