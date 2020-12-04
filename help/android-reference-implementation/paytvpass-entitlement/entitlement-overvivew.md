---
description: 권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.
seo-description: 권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.
seo-title: 권한 부여 관리자 개요
title: 권한 부여 관리자 개요
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# 권한 부여 관리자 개요 {#entitlement-manager-overview}

권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.

## 기능 개요

Android Primetime SDK 참조 구현과 Primetime 인증 통합을 통해 애플리케이션에 새로운 기능 관리자가 추가되었습니다. 그러나 다른 많은 기능 관리자와 달리 *EntitlementManager는 응용 프로그램 전체에서의 여러 위치에서 사용됩니다*. 다음은 Primetime 인증을 지원하기 위한 참조 구현의 변경 사항 및 추가 사항에 대한 개요입니다.

### EntitlementManager 클래스

`EntitlementManager` 클래스는 Primetime 인증 SDK와의 모든 통신을 처리하며 권한 부여 워크플로에 필요한 응용 프로그램 논리를 캡슐화합니다. `EntitlementManager`의 공개 API는 응용 프로그램이 권한 부여 워크플로우를 시작하는 데 사용되는 반면, `EntitlementMangerListener` 인터페이스는 응용 프로그램이 `EntitlementManger` 이벤트를 처리하는 콜백 메커니즘을 제공합니다.

### EntitlementManager 콜백

참조 구현의 기본 활동인 `CatalogActivity`은 `EntitlementManagerListener`의 인스턴스를 만들고 `EntitlementManager`에 등록합니다. 이러한 방식으로 `EntitlementManager`은 필요한 UI가 나머지 응용 프로그램에 업데이트되도록 신호를 보낼 수 있습니다. 콜백에는 로드 대화 상자 표시/숨기기, 상태 대화 상자 표시, 인증 및 인증 아이콘 업데이트, 승인 시 비디오 재생 시작 등이 포함됩니다.

### 권한 부여 대화 상자

`EntitlementDialogFragment` 클래스는 클래스 생성자에게 전달된 권한 상태를 기반으로 대화 상자 메시지를 생성합니다. 이 클래스는 모든 오류 메시지와 인증 성공 메시지에 사용됩니다. `CatalogActivity`은 `EntitlementManager`로부터 특정 이벤트를 받을 때 권한 대화 상자를 표시합니다. 또한 `CatalogActivity`은 대화 상자가 닫힐 때 또는 사용자가 Primetime 인증 서비스에서 로그아웃될 때 신호를 보내는 콜백 메서드를 포함하는 `EntitlementDialogListener` 인터페이스를 구현합니다.

### 컨텐츠 공급자 선택 및 로그인

Primetime 인증을 통해 인증하는 동안 두 개의 새로운 활동인 `MvpdPickerActivity` 및 `MvpdLoginActivity`이(가) 사용자가 컨텐트 제공자와 로그인을 선택할 수 있도록 합니다. 이 두 활동은 모두 `EntitlementManager`을 통해 `CatalogActivity`부터 시작됩니다. 또한 `MvpdPickerActivity` 및 `MvpdLoginActivity` 모두 `CatalogActivity`에 대한 결과를 반환하고 그에 따라 `CatalogActivity`은 `Activity.onActivityResult` 메서드를 재정의해야 합니다.

### 로그인 단추

참조 구현의 기본 활동인 `CatalogActivity`은 작업 표시줄에 새로운 &quot;로그인&quot; 단추를 포함합니다. 로그인 버튼을 사용하면 Primetime 인증을 통해 인증을 시작할 수 있습니다. 또한 사용자는 재생할 보호된 비디오를 선택하여 인증을 시작할 수 있습니다. 로그인 단추의 아이콘과 텍스트는 사용자의 인증 상태에 따라 변경되며, `CatalogActivity`에는 페이지가 새로 고쳐질 때 단추의 아이콘과 텍스트를 업데이트하는 코드가 포함되어 있습니다. 이 작업을 수행하려면 `CatalogActivity`이 시작되면 `EntitlementManager.checkAuthentication()`을(를) 호출하여 사용자의 인증 상태를 업데이트합니다.

### 콘텐츠 권한 부여

`CatalogView` 내에서 해당 컨텐츠에 대한 사용자의 인증 상태를 알리기 위해 새 아이콘이 컨텐츠 아이콘 위에 표시됩니다. 예를 들어 사용자가 비디오를 볼 수 있도록 사전 허가를 받은 경우 컨텐츠 위에 녹색 원 아이콘이 표시됩니다. 그러나 사용자가 비디오를 볼 수 있는 사전 권한이 없는 경우 키 아이콘이 표시됩니다. 이러한 아이콘의 표시는 `ContentTileAdapter`에서 처리되지만 `EntitlementManagerListener`의 콜백이 호출되면 `CatalogActivity`에서 해당 상태 업데이트가 시작됩니다.

### 컨텐츠 재생

이제 비디오를 재생하려면 `EntitlementManager`의 인증 검사가 필요합니다. `EntitlementManager.getAuthorization()`에 대한 호출이 `CatalogView` 내에서 발생합니다. 비디오에 인증이 필요하며 사용자가 인증되면 `PlayerActivity`은 `CatalogActivity`부터 시작됩니다.

