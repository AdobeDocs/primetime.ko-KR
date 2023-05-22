---
title: Android 10 앱에서 Enabler Android SDK SSO(Single Sign-On) 액세스
description: Android 10 앱에서 Enabler Android SDK SSO(Single Sign-On) 액세스
exl-id: dedade15-c451-4757-b684-d3728e11dd87
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Android 10 앱에서 Enabler Android SDK SSO(Single Sign-On) 액세스 {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

## 개요

Adobe Primetime 인증 기반 앱 간의 SSO(Single Sign-On)는 Access Enabler Android SDK를 통해 Android OS를 사용하는 디바이스에서 사용할 수 있습니다. Android 장치에서 SSO(Single Sign-On)를 제공하기 위해 Access Enabler Android SDK 버전 3.2.1(최신) 및 이전 버전은 Android 스토리지 구현에 저장된 공유 데이터베이스 파일을 사용하며 모든 Adobe Primetime 인증 기반 앱에서 액세스할 수 있습니다.

그러나 최신 Android 10 릴리스의 Google에서는 &quot;사용자에게 파일에 대한 더 많은 제어 권한을 부여하고 파일이 복잡하지 않도록 제한하기 위해 Android 10(API 레벨 29) 이상을 타깃팅하는 앱에 기본적으로 외부 저장 장치 또는 범위가 지정된 저장소에 대한 액세스 권한이 부여됩니다. 이러한 앱은 앱별 디렉터리만 볼 수 있습니다. `\[...\]`&quot;. 이러한 Android 10 스토리지 변경 사항과 관련된 자세한 내용은에 나와 있습니다 [Android용 데이터 및 파일 스토리지 설명서](https://developer.android.com/training/data-storage/files/external-scoped).

이러한 변경 사항으로 인해 Access Enabler Android 버전에서 제공하는 SSO(Single Sign-On)가 **3.2.1 SDK(최신)** 및 이전 버전은 다음 섹션에서 설명한 대로 Android 10 디바이스에서 영향을 받을 수 있습니다.

다음을 참조하십시오 [Roku SSO 개요](/help/authentication/roku-sso-overview.md).

## 비헤이비어

앱에 따라 **target SDK 수준** 또는 의 사용 **android:requestLegacyExternalStorage** manifest 특성 Access Enabler Android 버전 3.2.1 SDK(최신) 및 이전 버전에서 제공하는 SSO(Single Sign-On)는 현재 다음과 같이 동작합니다.

- 앱 타겟 **Android 9(API 레벨 28)** 또는 더 낮음 **-\>** SSO(단일 인증) **작동 예정**
- 앱 타겟 **안드로이드 10** **(API 레벨 29)** 및 **set** 값: **requestLegacyExternalStorage to true** 앱의 매니페스트 파일에서 **-\>** SSO(단일 인증) **작동 예정**
- 앱 타겟 **안드로이드 10** **(API 레벨 29)** 및 **설정되지 않음** 값: **requestLegacyExternalStorage to true** 앱의 매니페스트 파일에서 **-\>** SSO(단일 인증) **작동하지 않음**


>[!TIP]
>
> Adobe Primetime 인증 Access Enabler Android SDK가 범위 지정 스토리지와 완전히 호환되기 전에, 공개적으로 설명한 대로 앱의 대상 SDK 수준 또는 requestLegacyExternalStorage 매니페스트 특성을 기반으로 일시적으로 옵트아웃할 수 있습니다 [Android 설명서](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).
