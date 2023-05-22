---
description: 참조 구현을 사용자 정의하여 프로덕션 환경에 Adobe Primetime 인증을 통합합니다.
title: Primetime 인증 통합
exl-id: ef6dc75d-d00f-481f-a620-4ec402cbebb6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Primetime 인증 통합 {#integrate-primetime-authentication}

참조 구현을 사용자 정의하여 프로덕션 환경에 Adobe Primetime 인증을 통합합니다.

Primetime 인증 서비스의 참조 구현 통합은 데모로서 즉시 사용할 수 있습니다. 그러나 프로덕션 준비 플레이어에서 통합을 사용하려면 다음 사용자 지정을 구현해야 합니다.

1. 권리 유형 흐름을 활성화하거나 비활성화합니다.

   다음 `EntitlementManager` 활성화하려면 먼저 Primetime 인증 SDK의 인스턴스를 초기화하고 획득해야 합니다. 다음과 같은 경우 `EntitlementManager` 이 라이브러리를 초기화하지 않으면 관리자가 비활성화됩니다.
1. 활성화 `EntitlementManger`기본 애플리케이션 클래스에서 가져온 값:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. 사용 `ManagerFactory` 클래스의 인스턴스를 가져올 수 있습니다. `EntitlementManager`.

   항상 를 사용해야 합니다. `ManagerFactory` 의 인스턴스를 가져오려면 `EntitlementManager`를 로 사용 `ManagerFactory` 는 응용 프로그램에 대한 EntitlementManager의 단일 인스턴스를 유지 관리합니다. 인스턴스화 안 함 `EntitlementManager` 또는 `EntitlementManagerOn` 클래스 생성자를 사용하여 클래스를 만듭니다.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   다음 `ManagerFactory` 의 인스턴스를 반환합니다. `EntitlementManagerOn`을(를) 전에 호출한 경우 자격 흐름이 활성화된 상태로 `EntitlementManager.initializeAccessEnabler`. 먼저 전화하지 않으면 `EntitlementManager.initializeAccessEnabler`, 그런 다음 `ManagerFactory` 의 인스턴스를 반환합니다. `EntitlementManager`(권한 흐름이 비활성화되어 있음) 1. 요청자 ID를 구성합니다.

   참조 구현은 테스트 요청자 ID가 &quot;REF&quot;로 설정된 사전 구성된 상태로 제공됩니다. 이 요청자 ID를 사용하여 애플리케이션을 테스트할 수 있습니다. Primetime 인증 담당자가 제공한 요청자 ID를 사용할 준비가 되면 [!DNL res/values/strings.xml] 요청자 ID가 있는 파일입니다.

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   또한 애플리케이션이 Primetime 인증 서비스에 연결하는 데 사용하는 URL을 변경해야 할 수도 있습니다. 여기에는 Primetime 인증 스테이징 및 프로덕션 서버 URL과 토큰 확인 서비스의 URL이 포함됩니다. 자세한 내용은 Adobe Primetime 담당자에게 문의하십시오. 1. 요청자 ID에 서명

   Primetime 인증 시스템 내에서 프로그래머의 ID를 설정하기 위해 프로그래머의 요청자 ID가 Primetime 인증 시스템으로 전송됩니다. 보안 강화를 위해 요청자 ID는 Adobe으로 보내기 전에 프로그래머가 서명해야 합니다. Adobe은 프로그래머가 신뢰할 수 있는 네트워크에서 요청자 ID에 서명하도록 서비스를 설정할 것을 권장합니다.

   Primetime 참조 구현은 요청자 ID에 서명하는 방법을 보여 주지만, 이는 데모용으로만 사용됩니다. Adobe은 서명 인증서와 서명 생성기 코드를 `com.adobe.primetime.reference.crypto`는 프로덕션 애플리케이션 내에 포함해서는 안 됩니다. 대신 신뢰할 수 있는 네트워크 서비스로 이동해야 합니다.

1. 서버 환경을 구성합니다.

   Primetime 인증 서비스는 두 개의 개별 환경에서 실행할 수 있습니다.

   * 스테이징 - 스테이징 환경은 애플리케이션 테스트에 사용됩니다.
   * 프로덕션 - 프로덕션 환경은 애플리케이션의 라이브 배포에 사용됩니다.

   응용 프로그램을 사용하여 스테이징 및 프로덕션 환경 모두에 대한 URI를 설정하지만 코드 내에서 응용 프로그램에서 사용하는 URI 중 하나를 설정해야 합니다. 다음에서 `com.adobe.primetime.reference.manager.EntitlementManger` 클래스, 설정 `environmentUri` 변수를 다음 중 하나로 변환 `STAGING_URI` 또는 `PRODUCTION_URI` 사용 중인 Primetime 인증 서비스 환경에 따라 다릅니다.

   >[!NOTE]
   >
   >제공된 요청자 ID(&quot;REF&quot;)는 스테이징 환경에만 사용해야 합니다.

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
   
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
   
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
   
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
   
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. MVPD 선택 그리드를 사용자 지정합니다.

   콘텐츠 제공자 선택 페이지는 사용자가 선택할 수 있는 상위 9개의 MVPD들의 테이블을 표시한다. 이 애플리케이션은 Primetime 인증 시스템의 프로그래머와 통합된 사용 가능한 MVPD와 일치하는 애플리케이션 내의 정렬된 목록에서 상위 9개의 MVPD를 가져옵니다. 기본 MVPD의 순서가 지정된 목록은 MVPD 표시 이름이 아닌 Primetime 인증 시스템 내의 MVPD ID에 맞춰져 있습니다. 기본 MVPD 목록의 MVPD ID가 프로그래머 계정과 통합된 MVPD ID와 일치하는지 확인하는 것이 중요합니다. 경우에 따라 ID는 통합 간에 다를 수 있습니다. 다음은 클래스에 있는 기본 MVPD의 순서 목록입니다. `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   다음 표는 1차 MVPD의 순서가 지정된 목록을 사용하는 방법의 예를 제공합니다. 첫 번째 열에는 프로그래머와 통합된 MVPD가 나열되어 있다. 두 번째 열은 (축소된) MVPD 순서 목록입니다. 세 번째 열은 사용자에게 상위 6개의 MVPD를 표시하는 데 사용되는 결과 목록입니다.

   이 예제에서는 실제 9개 MVPD 대신 상위 6개의 MVPD를 사용하여 예제를 간단하게 만듭니다. 결과 목록에 처음 두 목록의 교차 지점이 포함되고 순서가 두 번째 목록과 어떻게 동일한지 확인합니다. 또한, AT&amp;T U-verse는 첫 번째로 일치하는 6개의 MVPD만 취하기 때문에 최종 목록에 없습니다.

| 사용 가능한 MVPD | 기본 MVPD | 표시된 MVPD 6개 |
|--- |--- |--- |
| <ol><li>컴캐스트 크기</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>접시</li><li>-</li><li>CableOne</li><li>브라이트하우스</li><li>대서양 광대역</li><li>와우!</li><li>MetroCast</li><li>다이렉트 </li><li>콕스</li><li>케이블 비전 최적</li></ol> | <ol><li>컴캐스트 크기</li><li>다이렉트</li><li>접시</li><li> TWC</li><li>콕스</li><li>헌장</li><li>버라이즌</li><li>케이블 비전 최적</li><li>-</li></ol> | <ol><li>컴캐스트 크기</li><li>다이렉트</li><li>접시</li><li>TWC</li><li>콕스</li><li>케이블 비전 최적</li></ol> |
