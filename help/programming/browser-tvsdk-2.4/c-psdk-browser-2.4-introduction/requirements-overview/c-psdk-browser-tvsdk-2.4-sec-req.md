---
description: 브라우저 TVSDK에 대해 알아 두어야 할 몇 가지 보안 고려 사항이 있습니다.
title: 보안 고려 사항
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 보안 고려 사항{#security-considerations}

브라우저 TVSDK에 대해 알아 두어야 할 몇 가지 보안 고려 사항이 있습니다.

* **Adobe Flash Player**

   * Flash Player은 SWF이 시작된 도메인 외부에 있는 데이터에 대한 액세스를 허용하지 않습니다.

     액세스를 허용하려면 데이터를 호스팅하는 서버의 루트에 적절한 권한이 있는 도메인 간 정책 파일을 호스팅하십시오. 브라우저 TVSDK(Flash Player 버전 23 이상)의 Flash 대체 모드에서는 도메인에 대한 인증 토큰이 필요합니다. 토큰을 생성하려면 Adobe 담당자에게 문의하십시오.

* **JavaScript**

   * JavaScript는 동일한 원본 정책을 따르며 도메인 경계를 넘어 리소스에 대한 액세스를 차단합니다.

     이러한 리소스에 대한 액세스를 허용하려면 플레이어 이외의 원본에서 호스팅되는 리소스에 CORS(Access-Control-Allow-Origin) 헤더를 설정해야 합니다. 선택적으로 바이트 범위를 사용하여 콘텐츠를 지정하는 경우 CORS 사전 플라이트 옵션 요청은 이러한 요청이 원점에서 허용됨을 나타내야 합니다.

* **브라우저 및 혼합 컨텐츠**

   * 브라우저에서는 AES-128 암호화 콘텐츠를 보안 원본(예: HTTPS)을 통해 호스팅해야 합니다.

     대부분의 브라우저는 혼합 콘텐츠를 허용하지 않으므로 플레이어, 콘텐츠 및 Key/WebVTT 파일과 같은 관련 에셋도 보안 원본 을 통해 호스팅되는 것이 좋습니다.

     >[!IMPORTANT]
     >
     >버전 2.4.5부터 플레이어가 HTTPS를 통해 호스팅되는 경우 브라우저 TVSDK는 MSE 기술을 사용할 때 HTTP 호출을 HTTPS로 변환합니다.
