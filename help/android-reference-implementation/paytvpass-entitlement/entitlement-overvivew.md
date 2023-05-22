---
description: 권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.
title: 권한 부여 관리자 개요
exl-id: a66e131e-283f-4378-b834-7cfa887b3ec9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# 권한 부여 관리자 개요 {#entitlement-manager-overview}

권한 부여 관리자는 Primetime 인증 구현을 지원하는 기능 관리자입니다.

## 기능 개요

Android Primetime SDK 참조 구현과 Primetime 인증 통합으로 애플리케이션에 새로운 기능 관리자가 추가됩니다. 그러나 다른 많은 기능 관리자와 달리 *EntitlementManager는 응용 프로그램 전체에서 여러 위치에 사용됩니다*. 다음은 Primetime 인증을 지원하기 위해 참조 구현에서 수행된 변경 사항과 추가 사항에 대한 개요를 제공합니다.

### EntitlementManager 클래스

다음 `EntitlementManager` 클래스는 Primetime 인증 SDK와의 모든 통신을 처리하며 권한 부여 워크플로에 필요한 애플리케이션 논리를 캡슐화합니다. 다음 `EntitlementManager`의 공개 API는 애플리케이션에서 권리 유형 워크플로를 시작하는 데 사용되지만 `EntitlementMangerListener` 인터페이스는 응용 프로그램에서 처리할 콜백 메커니즘을 제공합니다 `EntitlementManger` 이벤트.

### EntitlementManger 콜백

참조 구현의 기본 활동인 `CatalogActivity`, 의 인스턴스를 만듭니다. `EntitlementManagerListener` 을(를) 등록 `EntitlementManager`. 이렇게 하면 `EntitlementManager` 는 나머지 애플리케이션에 필요한 UI 업데이트를 알릴 수 있습니다. 콜백에는 로드 대화 상자 표시/숨기기, 상태 대화 상자 표시, 권한 부여 및 인증 아이콘 업데이트, 권한 부여가 완료되면 비디오 재생 시작 등이 포함됩니다.

### 권한 부여 대화 상자

다음 `EntitlementDialogFragment` 클래스는 클래스 생성자에 전달된 권한 상태에 따라 대화 상자 메시지를 생성합니다. 이 클래스는 모든 오류 메시지뿐만 아니라 인증 성공 메시지에 사용됩니다. 다음 `CatalogActivity` 에서 특정 이벤트를 수신할 때 권한 대화 상자를 표시합니다. `EntitlementManager`. 또한 `CatalogActivity` 를 구현합니다. `EntitlementDialogListener` 인터페이스를 포함합니다. 이 인터페이스에는 대화 상자가 닫히거나 사용자가 Primetime 인증 서비스에서 로그아웃할 때 신호를 보내는 콜백 메서드가 포함됩니다.

### 콘텐츠 공급자 선택 및 로그인

Primetime 인증을 사용하여 인증하는 동안 두 개의 새 활동이 `MvpdPickerActivity` 및 `MvpdLoginActivity`을 통해 사용자는 콘텐츠 공급자를 선택하고 로그인할 수 있습니다. 이 두 활동은 모두에서 시작됩니다. `CatalogActivity` 를 통해 `EntitlementManager`. 또한 `MvpdPickerActivity` 및 `MvpdLoginActivity` 에 결과 반환 `CatalogActivity` 및 그 때문에 `CatalogActivity` 은(는) 을(를) 재정의해야 합니다. `Activity.onActivityResult` 메서드를 사용합니다.

### 로그인 단추

참조 구현의 기본 활동인 `CatalogActivity`에는 작업 표시줄에 새로운 &quot;로그인&quot; 버튼이 포함되어 있습니다. 로그인 버튼을 사용하면 Primetime 인증을 통해 인증을 시작할 수 있습니다. 추가적으로, 사용자는 재생하기 위해 보호된 비디오를 선택함으로써 인증을 개시할 수 있다. 로그인 버튼의 아이콘 및 텍스트는 사용자의 인증 상태 및 `CatalogActivity` 페이지를 새로 고칠 때 단추의 아이콘과 텍스트를 업데이트하는 코드가 포함되어 있습니다. 다음을 수행하는 경우 `CatalogActivity` 시작, 호출 `EntitlementManager.checkAuthentication()` 을 클릭하여 사용자의 인증 상태를 업데이트합니다.

### 콘텐츠 권한

다음 범위 내 `CatalogView`, 콘텐츠의 아이콘 위에 해당 콘텐츠에 대한 사용자의 인증 상태를 알리는 새 아이콘이 표시됩니다. 예를 들어, 사용자가 비디오를 볼 수 있는 권한이 있는 경우 컨텐츠 위에 녹색 원 아이콘이 표시됩니다. 그러나 사용자가 비디오를 볼 수 있는 사전 권한이 없는 경우에는 키 아이콘이 표시됩니다. 이러한 아이콘의 표시는에서 처리됩니다. `ContentTileAdapter`, 그러나 상태 업데이트는 `CatalogActivity` 에서 콜백을 수행하는 경우 `EntitlementManagerListener` 이(가) 호출되었습니다.

### 컨텐츠 재생

이제 비디오 재생에는 `EntitlementManager`. 에 대한 호출 `EntitlementManager.getAuthorization()` 다음 범위 내에서 발생 `CatalogView`. 비디오에 인증이 필요하고 사용자에게 권한이 부여된 경우 `PlayerActivity` 다음에서 시작: `CatalogActivity`.
