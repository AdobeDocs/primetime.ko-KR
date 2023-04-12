---
title: Android 10 앱에서 Android SDK SSO(Single Sign-On)에 액세스
description: Android 10 앱에서 Android SDK SSO(Single Sign-On)에 액세스
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---



# Android 10 앱에서 Android SDK SSO(Single Sign-On)에 액세스 {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요

Adobe Primetime 인증 기반 앱 간의 SSO(Single Sign-On)는 Access Enabler Android SDK를 통해 Android OS를 사용하는 장치에서 사용할 수 있습니다. Android 장치에서 SSO(Single Sign-On)를 제공하기 위해 Access Enabler Android SDK 버전 3.2.1(최신) 및 이전 버전은 모든 Adobe Primetime 인증 기반 앱에서 액세스할 수 있는 Android 스토리지 구현에 저장된 공유 데이터베이스 파일을 사용합니다.

그러나 최신 Android 10 릴리스의 Google은 &quot;사용자에게 파일을 보다 세밀하게 제어하고 파일 불량을 제한하기 위해 일부 변경 사항을 생성했으며, Android 10(API 레벨 29) 이상을 대상으로 하는 앱에 기본적으로 외부 스토리지 장치 또는 범위 지정 스토리지에 대한 액세스 범위가 지정됩니다. 이러한 앱은 앱별 디렉터리만 볼 수 있습니다 `\[...\]`&quot;. 이러한 Android 10 스토리지 변경 사항과 관련된 자세한 내용은 [Android용 데이터 및 파일 저장소 설명서](https://developer.android.com/training/data-storage/files/external-scoped).

이러한 변경 결과로 Access Enabler Android 버전에서 제공하는 SSO(Single Sign-On)가 변경됩니다 **3.2.1 SDK (최신)** 및 이전 버전은 다음 섹션에 설명된 대로 Android 10 장치에서 영향을 받을 수 있습니다.

자세한 내용은 [Roku SSO 개요](/help/authentication/roku-sso-overview.md).

## 비헤이비어

앱의 **target SDK 수준** 또는 **android:requestLegacyExternalStorage** manifest 속성은 Access Enabler Android 버전 3.2.1 SDK(최신) 및 이전 버전에서 제공하는 SSO(Single Sign-On)가 현재 다음과 같이 동작합니다.

- 앱 타겟 **Android 9(API 레벨 28)** 이하 **-\>** 단일 사인온(SSO) **작업**
- 앱 타겟 **Android 10** **(API 수준 29)** 및 **설정** 의 값 **requestLegacyExternalStorage가 true로 설정됨** 앱 매니페스트 파일에서 **-\>** 단일 사인온(SSO) **작업**
- 앱 타겟 **Android 10** **(API 수준 29)** 및 **설정되지 않음** 의 값 **requestLegacyExternalStorage가 true로 설정됨** 앱 매니페스트 파일에서 **-\>** 단일 사인온(SSO) **작동하지 않음**


>[!TIP]
>
> Adobe Primetime 인증 Access Enabler Android SDK가 범위 지정 스토리지와 완전히 호환되기 전에 공개 설명에 따라 앱의 target SDK 수준 또는 requestLegacyExternalStorage 매니페스트 속성을 기반으로 일시적으로 옵트아웃할 수 있습니다 [Android 설명서](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).

