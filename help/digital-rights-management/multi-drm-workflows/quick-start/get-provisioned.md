---
description: ExpressPlay 기반의 Primetime DRM Cloud를 시작하려면 Adobe 담당자의 도움을 받아 Adobe Cert 및 ExpressPlay 계정을 설정해야 합니다.
seo-description: ExpressPlay 기반의 Primetime DRM Cloud를 시작하려면 Adobe 담당자의 도움을 받아 Adobe Cert 및 ExpressPlay 계정을 설정해야 합니다.
seo-title: 제공 받기(계정 등)
title: 제공 받기(계정 등)
uuid: 51b95676-2121-4d8b-8756-9fd097185a13
translation-type: tm+mt
source-git-commit: 9792aff8586c46aabb5bfb70864cfe98c28e602d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 프로비전됨(계정 등) {#get-provisioned-accounts-etc}

ExpressPlay 기반의 Primetime DRM Cloud를 시작하려면 Adobe 담당자의 도움을 받아 Adobe Cert 및 ExpressPlay 계정을 설정해야 합니다.

1. TVSDK를 사용하여 다중 DRM을 구현하는 데 필요한 Adobe Cert 및 ExpressPlay 계정을 Adobe 담당자에게 요청하십시오.

       Adobe 담당자에게 연락처로 사용할 이메일 주소를 제공하십시오. 그런 다음 Adobe에서 두 개의 계정을 만듭니다.
   
   * ***인증서 포털 계정***  - ( <span></span>https://certportal.primetime.adobe.com):Adobe 액세스/Primetime DRM 인증서  *등록 관리* 팀은 제공한 주소로 이메일을 보냅니다. 이 이메일에는 Adobe 인증서 등록 설명서에 대한 링크와 함께 Adobe 인증서 포털용 URL이 포함되어 있습니다(최신 문서는 여기에 있습니다.[인증서 등록 안내서](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***ExpressPlay 계정***  - Adobe은 ExpressPlay 관리자 계정에 등록하는 데 사용하는 링크가 포함된 이메일을 보냅니다.

1. Adobe ID을 사용하여 Adobe 인증서 포털에 로그인합니다(Adobe 담당자에게 제공한 것과 동일한 이메일 주소 사용). 아직 Adobe ID이 없는 경우 인증서 포털에서 *Adobe ID 가져오기* 링크를 따라 신속하게 만들 수 있습니다.

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. Adobe 인증서 포털에서 *시험버전* 인증서를 요청합니다.

   멀티 DRM 시험버전의 경우 단일 시험버전으로 컨텐츠 보호 기능이 다음과 같은 모든 측면을 다룹니다.패키징, 라이선스 및 전송 인증서를 요청하려면 자신의 [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md)을(를) 제공해야 합니다.
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe은 인증서 요청의 수락 또는 거부를 나타내는 이메일을 사용자에게 보냅니다. 인증서 포털의 *요청 내역* 탭에서 인증서 요청의 상태를 볼 수 있습니다.
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. ExpressPlay 관리자 계정을 만듭니다.

   해당 Adobe이 제공한 ExpressPlay 링크를 따릅니다. 그러면 ExpressPlay에서 *계정 만들기* 페이지가 열립니다. 필요한 정보를 입력하고 양식을 제출합니다. 1주일 동안 유효한 활성화 링크가 포함된 `operations@expressplay.com`의 이메일을 받게 됩니다. 활성화한 후 ExpressPlay 서비스를 설정합니다.
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   서비스를 만들면 고유한 관리 페이지가 표시됩니다. 일부 활동 추적 필드와 함께, 프로덕션 및 테스트 *고객 인증자*(API 키) 및 프로덕션 및 테스트 서비스 URL이 표시됩니다.

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. FairPlay를 사용하는 경우 Apple 개발자 사이트에서 ExpressPlay를 설정하는 추가 단계가 포함됩니다. 지침은 [FairPlay용 ExpressPlay 서비스 활성화](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay)를 참조하십시오.
