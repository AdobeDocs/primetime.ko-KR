---
description: 브라우저 TVSDK에 대해 알아야 할 몇 가지 보안 고려 사항이 있습니다.
title: 보안 고려 사항
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# 보안 고려 사항{#security-considerations}

브라우저 TVSDK에 대해 알아야 할 몇 가지 보안 고려 사항이 있습니다.

* **Adobe Flash Player**

   * Flash Player에서는 SWF가 시작된 도메인 외부에 있는 데이터에 대한 액세스를 허용하지 않습니다.

      액세스를 허용하려면 데이터를 호스팅하는 서버의 루트에 적절한 권한이 있는 크로스 도메인 정책 파일을 호스트합니다. 브라우저 TV SDK(Flash Player 버전 23 이상)의 Flash 폴백 모드에서는 도메인에 대한 인증 토큰이 필요합니다. 토큰을 생성하려면 Adobe 담당자에게 문의하십시오.

* **JavaScript**

   * JavaScript는 동일한 원본 정책을 따르며 도메인 경계를 넘어 리소스에 액세스할 수 없습니다.

      이러한 리소스에 대한 액세스를 허용하려면 CORS(Access-Control-Allow-Origin) 헤더는 플레이어가 아닌 원본 리소스에 대해 설정되어야 합니다. 필요에 따라 바이트 범위를 사용하여 컨텐츠를 지정하는 경우 CORS 프리플라이트 옵션 요청은 이러한 요청이 원점에서 허용됨을 나타내야 합니다.

* **브라우저 및 혼합 컨텐츠**

   * 브라우저에서는 보안 원본(예: HTTPS)을 통해 AES-128로 암호화된 내용을 호스팅해야 합니다.

      대부분의 브라우저에서는 혼합 컨텐츠를 허용하지 않으므로 플레이어, 컨텐츠 및 Key/WebVTT 파일과 같은 관련 에셋도 보안 원본 파일을 통해 호스팅되는 것이 좋습니다.

      >[!IMPORTANT]
      >
      >버전 2.4.5부터, 플레이어가 HTTPS를 통해 호스팅되는 경우 MSE 기술을 사용할 때 브라우저 TVSDK는 HTTP 호출을 HTTPS로 변환합니다.

