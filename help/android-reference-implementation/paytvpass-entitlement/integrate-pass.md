---
description: 제작 환경에 Adobe Primetime 인증을 통합하기 위해 참조 구현을 사용자 정의합니다.
title: Primetime 인증 통합
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---


# Primetime 인증 통합 {#integrate-primetime-authentication}

제작 환경에 Adobe Primetime 인증을 통합하기 위해 참조 구현을 사용자 정의합니다.

Primetime 인증 서비스의 참조 구현 통합은 데모로 즉시 작동합니다. 그러나 프로덕션 준비 플레이어에서 통합을 사용하려면 다음 사용자 지정을 구현해야 합니다.

1. 권한 부여 흐름을 활성화 또는 비활성화합니다.

   `EntitlementManager`은(는) 먼저 초기화하여 Primetime 인증 SDK의 인스턴스를 받아야 합니다. `EntitlementManager`이(가) 이 라이브러리를 초기화하지 않으면 관리자가 비활성화됩니다.
1. 기본 응용 프로그램 클래스에서 `EntitlementManger`을 활성화합니다.

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. `ManagerFactory` 클래스를 사용하여 `EntitlementManager` 인스턴스를 가져옵니다.

   `ManagerFactory`에서 응용 프로그램에 대한 EntitlementManager의 단일 인스턴스를 유지 관리하므로 항상 `ManagerFactory`을 사용하여 `EntitlementManager` 인스턴스를 가져와야 합니다. 생성자를 사용하여 `EntitlementManager` 또는 `EntitlementManagerOn` 클래스를 인스턴스화하지 마십시오.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   이전에 `EntitlementManager.initializeAccessEnabler`을(를) 호출한 경우 `ManagerFactory`은 권한 흐름이 활성화된 `EntitlementManagerOn` 인스턴스를 반환합니다. `EntitlementManager.initializeAccessEnabler`을(를) 처음 호출하지 않으면 `ManagerFactory`은 `EntitlementManager`의 인스턴스를 반환하고 권한 흐름이 비활성화됩니다. 1. 요청자 ID를 구성합니다.

   참조 구현은 테스트 요청자 ID가 다음으로 설정된 사전 구성되어 있습니다.&quot;참조&quot;. 이 요청자 ID를 사용하여 응용 프로그램을 테스트할 수 있습니다. Primetime 인증 담당자가 제공한 요청자 ID를 사용할 준비가 되면 요청자 ID로 애플리케이션의 [!DNL res/values/strings.xml] 파일을 업데이트하십시오.

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

   또한 애플리케이션이 Primetime 인증 서비스에 연결하는 데 사용하는 URL을 변경해야 할 수 있습니다. 여기에는 Primetime 인증 스테이징 및 프로덕션 서버 URL과 토큰 확인 서비스에 대한 URL이 포함됩니다. 자세한 내용은 Adobe Primetime 담당자에게 문의하십시오. 1. 요청자 ID에 서명합니다.

   Primetime 인증 시스템에서 프로그래머 ID를 확인하기 위해 프로그램 제작자의 요청자 ID를 Primetime 인증 시스템으로 보냅니다. 보안 레이어로 추가되어 있는 요청자 ID는 Adobe으로 보내기 전에 프로그래머에 의해 서명되어야 합니다. Adobe은 프로그래머가 신뢰할 수 있는 네트워크의 요청자 ID에 서명하도록 서비스를 설정하는 것이 좋습니다.

   Primetime 참조 구현에서는 요청자 ID에 서명하는 방법을 보여 주지만 이것은 데모용으로만 사용됩니다. Adobe은 `com.adobe.primetime.reference.crypto` 아래의 서명 인증서와 서명 생성기 코드를 프로덕션 응용 프로그램에 포함시키지 않는 것이 좋습니다. 대신 신뢰할 수 있는 네트워크 서비스로 전환해야 합니다.

1. 서버 환경 구성을 참조하십시오.

   Primetime 인증 서비스는

   * 스테이징 - 스테이징 환경은 응용 프로그램을 테스트하는 데 사용됩니다.
   * 프로덕션 - 프로덕션 환경은 애플리케이션의 라이브 배포에 사용됩니다.

   애플리케이션을 사용하여 스테이징 환경과 프로덕션 환경 모두에 대한 URI를 설정하지만 코드 내에서 응용 프로그램에서 사용하는 URI를 설정해야 합니다. `com.adobe.primetime.reference.manager.EntitlementManger` 클래스에서 사용 중인 Primetime 인증 서비스 환경에 따라 `environmentUri` 변수를 `STAGING_URI` 또는 `PRODUCTION_URI` 중 하나로 설정합니다.

   >[!NOTE]
   >
   >제공된 요청자 ID(&quot;REF&quot;)는 스테이징 환경에서만 사용해야 합니다.

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

1. MVPD 선택 격자 사용자 지정을 참조하십시오.

   컨텐트 공급자 선택 페이지에는 사용자가 선택할 수 있는 상위 9개 MVPD의 표가 표시됩니다. 이 애플리케이션은 Primetime 인증 시스템의 프로그래머와 통합된 사용 가능한 MVPD와 일치하는 애플리케이션 내의 순서가 지정된 목록에서 상위 9개의 MVPD를 가져옵니다. 기본 MVPD 목록이 Primetime 인증 시스템 내의 MVPD ID에 입력되어 있으며 MVPD 표시 이름이 아닙니다. MVPD 목록의 MVPD ID가 프로그래머 계정과 통합된 MVPD ID와 일치하는지 확인하는 것이 중요합니다. 경우에 따라 ID가 통합 간에 다를 수 있습니다. 다음은 `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment` 클래스에 있는 기본 MVPD의 순차 목록입니다.

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

   다음 표는 기본 MVPD의 순서가 지정된 목록을 사용하는 방법의 예를 제공합니다. 첫 번째 열에는 Programmer와 통합된 MVPD가 나열됩니다. 두 번째 열은 MVPD의 (단축) 순차 목록입니다. 세 번째 열은 사용자에게 상위 6개의 MVPD를 표시하는 데 사용되는 결과 목록입니다.

   이 예에서는 예제를 단순화하기 위해 실제 9개 대신 상위 6개 MVPD를 사용합니다. 결과 목록에 처음 두 목록의 교차 부분이 포함되고 두 번째 목록과 동일한 순서가 있습니다. 또한 첫 번째 일치하는 6개의 MVPD만 수행되므로 AT&amp;T U-B가 최종 목록에 없습니다.

| 사용 가능한 MVPD | 기본 MVPD | 6개의 MVPD가 표시됨 |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>디시</li><li>AT&amp;T 우시</li><li>CableOne</li><li>브리트하우스</li><li>Atlantic Broadband</li><li>와!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>케이블비전 최적</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>디시</li><li> TWC</li><li>Cox</li><li>차터</li><li>Verizon FiOS</li><li>케이블비전 최적</li><li>AT&amp;T 우시</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>디시</li><li>TWC</li><li>Cox</li><li>케이블비전 최적</li></ol> |
