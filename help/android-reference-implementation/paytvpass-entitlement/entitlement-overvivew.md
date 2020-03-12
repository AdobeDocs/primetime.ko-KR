---
description: 권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.
seo-description: 권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.
seo-title: 권한 부여 관리자 개요
title: 권한 부여 관리자 개요
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 권한 부여 관리자 개요 {#entitlement-manager-overview}

권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.

## 기능 개요

Android Primetime SDK Reference Implementation과 Primetime 인증 통합을 통해 애플리케이션에 새로운 기능 관리자가 추가되었습니다. 그러나 다른 많은 기능 관리자와 달리 EntitlementManager *는 애플리케이션*&#x200B;전체에서 여러 곳에서 사용됩니다. 다음은 Primetime 인증을 지원하기 위한 참조 구현의 변경 사항 및 추가 사항에 대한 개요를 제공합니다.

### EntitlementManager 클래스

이 `EntitlementManager` 클래스는 Primetime 인증 SDK를 사용하여 모든 통신을 처리하며 권한 부여 워크플로우에 필요한 애플리케이션 로직을 캡슐화합니다. 응용 프로그램에서 `EntitlementManager`권한 부여 워크플로우를 시작하는 데 응용 프로그램의 공개 API를 사용하는 반면 `EntitlementMangerListener` 인터페이스는 응용 프로그램에서 `EntitlementManger` 이벤트를 처리하는 콜백 메커니즘을 제공합니다.

### EntitlementManager 콜백

참조 구현의 기본 활동, 즉 `CatalogActivity`를 사용하면 인스턴스가 `EntitlementManagerListener` 생성되어 에 등록합니다 `EntitlementManager`. 이러한 방식으로, 필요한 UI가 애플리케이션의 나머지 부분에 업데이트될 `EntitlementManager` 수 있음을 알리는 메시지가 표시될 수 있습니다. 콜백에는 로드 대화 상자 표시/숨기기, 상태 대화 상자 표시, 인증 및 인증 아이콘 업데이트, 승인 시 비디오 재생 시작 등이 포함됩니다.

### 권한 부여 대화 상자

이 `EntitlementDialogFragment` 클래스는 클래스 생성자에게 전달된 권한 상태를 기반으로 대화 상자 메시지를 생성합니다. 이 클래스는 모든 오류 메시지와 인증 성공 메시지에 사용됩니다. 에서 `CatalogActivity` 특정 이벤트를 받으면 권한 대화 상자가 표시됩니다 `EntitlementManager`. 또한 이 `CatalogActivity` 인터페이스는 `EntitlementDialogListener` 구현되어 대화 상자가 닫혔거나 사용자가 Primetime 인증 서비스에서 로그아웃되었을 때 신호를 보내는 콜백 메서드가 포함되어 있습니다.

### 컨텐츠 공급자 선택 및 로그인

Primetime 인증을 통해 인증하는 동안 두 개의 새로운 `MvpdPickerActivity` 활동이 `MvpdLoginActivity`제공되므로 사용자는 자신의 컨텐츠 제공업체를 선택하고 로그인할 수 있습니다. 이 두 활동은 모두 를 통해 `CatalogActivity` 시작됩니다 `EntitlementManager`. 또한, `MvpdPickerActivity` 및 `MvpdLoginActivity` 반환 결과는 `CatalogActivity` 및 그에 따라 모두 메서드를 재정의해야 `CatalogActivity` 합니다 `Activity.onActivityResult` .

### 로그인 단추

참조 구현의 기본 활동인 `CatalogActivity`에 작업 표시줄에 새로운 &quot;로그인&quot; 단추가 포함됩니다. 로그인 버튼을 사용하면 Primetime 인증을 통해 인증을 시작할 수 있습니다. 또한 사용자는 보호된 비디오를 선택하여 재생을 시작할 수 있습니다. 로그인 단추의 아이콘과 텍스트는 사용자의 인증 상태에 따라 변경되며, 페이지가 새로 고쳐질 때 단추의 아이콘과 텍스트를 업데이트하는 코드가 `CatalogActivity` 포함되어 있습니다. 이렇게 하려면, `CatalogActivity` 시작 시 사용자의 인증 상태를 `EntitlementManager.checkAuthentication()` 업데이트해야 합니다.

### 콘텐츠 권한 부여

컨텐츠 아이콘 `CatalogView`위에 해당 컨텐츠에 대한 사용자의 인증 상태를 알리는 새 아이콘이 표시됩니다. 예를 들어 사용자가 비디오를 볼 수 있도록 사전 권한이 부여된 경우 컨텐츠 위에 녹색 원 아이콘이 표시됩니다. 그러나 사용자가 비디오를 볼 수 있는 사전 권한이 없으면 키 아이콘이 표시됩니다. 이러한 아이콘의 표시는 에서 `ContentTileAdapter`처리되지만 상태 업데이트는 콜백이 호출될 `CatalogActivity` 때 시작됩니다 `EntitlementManagerListener` .

### 컨텐츠 재생

이제 비디오를 재생하려면 에서 인증 검사를 수행해야 `EntitlementManager`합니다. 호출은 `EntitlementManager.getAuthorization()` 내부에서 `CatalogView`발생합니다. 비디오에 인증이 필요하고 사용자가 인증되면 `PlayerActivity` 에서 시작됩니다 `CatalogActivity`.

