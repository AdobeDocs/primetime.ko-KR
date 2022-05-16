---
description: ExpressPlay에서 제공하는 Primetime DRM Cloud를 시작하려면 Adobe 담당자의 도움을 받아 Adobe 인증서 및 ExpressPlay 계정을 설정해야 합니다.
title: 프로비저닝(계정 등)
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# 프로비저닝(계정 등) {#get-provisioned-accounts-etc}

ExpressPlay에서 제공하는 Primetime DRM Cloud를 시작하려면 Adobe 담당자의 도움을 받아 Adobe 인증서 및 ExpressPlay 계정을 설정해야 합니다.

1. Adobe 담당자에게 문의하여 TVSDK를 사용하여 다중 DRM을 구현하는 데 필요한 Adobe 인증서 및 ExpressPlay 계정을 요청하십시오.

   Adobe 담당자에게 연락처로 사용할 이메일 주소를 제공합니다. 그런 다음 두 개의 계정을 만듭니다.

   * ***인증서 포털 계정*** - ( https://certportal.primetime.adobe.com) : 다음 *Adobe 액세스/Primetime DRM 인증서 등록 관리 팀* 제공한 주소로 이메일을 보냅니다. 전자 메일에는 Adobe의 인증서 등록 설명서에 대한 링크와 함께 Adobe 인증서 포털용 URL이 포함되어 있습니다(최신 문서는 다음과 같습니다. [인증서 등록 안내서](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***ExpressPlay 계정*** - Adobe이 ExpressPlay 관리자 계정에 등록하는 데 사용하는 링크가 포함된 이메일을 보냅니다.

1. Adobe ID을 사용하여 Adobe 인증서 포털에 로그인합니다(Adobe 담당자에게 제공한 것과 동일한 이메일 주소를 사용). 아직 Adobe ID이 없다면 다음을 수행하여 빠르게 만들 수 있습니다 *Adobe ID 가져오기* 인증서 포털에서 연결:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. Adobe 인증서 포털에서 *체험판* 인증서

   다중 DRM 평가판의 경우 단일 평가판 인증서는 콘텐츠 보호의 모든 측면을 다룹니다. 패키지, 라이센스 및 전송 직접 공급하셔야 합니다 [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) 인증서를 요청하려면 다음을 수행하십시오.
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe이 인증서 요청의 수락 또는 거부를 나타내는 이메일을 보냅니다. 에서 인증서 요청의 상태를 볼 수 있습니다 *요청 기록* 인증서 포털의 탭:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. ExpressPlay 관리자 계정을 만듭니다.

   제공된 ExpressPlay Adobe에 대한 링크를 따르십시오. 이렇게 하면 *계정 만들기* ExpressPlay에서 페이지를 참조하십시오. 필요한 정보를 입력하고 양식을 제출하십시오. 에서 전자 메일을 받게 됩니다. `operations@expressplay.com` 일주일 동안 유효한 활성화 링크가 포함되어 있습니다. 활성화한 후 ExpressPlay 서비스를 설정합니다.
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   서비스를 만들면 자체 관리 페이지가 표시됩니다. 일부 활동 추적 필드와 함께 프로덕션 및 테스트가 표시됩니다 *고객 인증자* (API 키) 및 프로덕션 및 테스트 서비스 URL:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. FairPlay를 사용하는 경우 ExpressPlay를 설정하는 추가 단계(Apple 개발자 사이트에서)가 포함되어 있습니다. 자세한 내용은 [FairPlay에 ExpressPlay 서비스 사용](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) 참조하십시오.
