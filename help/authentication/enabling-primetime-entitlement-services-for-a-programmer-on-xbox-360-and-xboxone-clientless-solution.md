---
title: Xbox 360 및 XboxOne Clientless에서 프로그램에 대한 Primetime 자격 부여 서비스 활성화
description: Xbox 360 및 XboxOne Clientless에서 프로그램에 대한 Primetime 자격 부여 서비스 활성화
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Xbox 360 및 XboxOne Clientless에서 프로그램에 대한 Primetime 자격 부여 서비스 활성화 {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.




1. Programmer는 다음 정보를 제공하여 Primetime 인증 클라이언트 없는 솔루션용 Xbox 360/One을 활성화하는 Zendesk 티켓을 만듭니다.

   1. 플랫폼: 예: Xbox 360, Xbox One

   1. 요청자 ID: 예: netgeo, CNN 등

1. Adobe이 X509 인증서를 만들고 개인 키와 암호를 끝에 구성합니다.

1. Adobe은 티켓 또는 이메일을 통해 프로그래밍 자에게 공개 인증서(X509 인증서)를 제공합니다.

1. 그러면 프로그래머는 Microsoft에 등록된 앱의 GDNP 포털에 해당 공개 인증서를 설치해야 합니다.

1. 그러면 프로그래머가 Microsoft Xbox Live 서비스에서 XboxOne 또는 360용 JWT(Java Web Token) 또는 STS 토큰을 요청하며, 이 토큰은 3단계에서 제공하는 X509 공개 인증서를 사용하여 암호화됩니다.

1. Xbox 장치에 대한 고유한 deviceId가 포함된 토큰입니다. 다음과 같이 &#39;x&#39; 매개 변수를 사용하여 인증 헤더에 토큰(JWT 또는 STS)을 포함합니다.

   1. Xbox 360의 경우 Primetime 유료 TV 인증으로 전송하기 전에 XSTS 토큰이 Base64로 인코딩되어야 합니다.
   1. Xbox One의 경우 JWT가 이미 올바르게 인코딩되어 있으므로 추가 인코딩이 발생하지 않아야 합니다. 

1. Xbox 장치의 모든 API 호출에는 x 매개 변수에 위에 언급된 토큰이 있는 인증 헤더가 포함되어야 합니다.

 

>[!NOTE]
>
>특히 Xbox에는 디지털 서명과 관련된 몇 가지 고유한 요구 사항이 있습니다. XBox 콘솔의 장치 ID는 XSTS 토큰에 포함됩니다.  Xbox 360의 경우 암호화된 SAML 검증입니다. Xbox One의 경우 암호화된 JWT입니다. XBox 콘솔 앱은 전체 XSTS 토큰을 Primetime 유료 TV 인증에 보냅니다. Primetime 유료 TV 인증은 공개 키를 사용하여 토큰을 해독하고, 토큰을 구문 분석하고, 해당 인증서에서 deviceId를 추출합니다.

>[!NOTE]
>
>XSTS 토큰의 길이가 커서 XBox 콘솔에는 다음과 같은 기술적 제한이 있습니다. 토큰을 HTTP GET 매개 변수로 Primetime 유료 TV 인증 API에 보낼 수 없습니다. 이를 해결하기 위해 Primetime 유료 TV 인증을 사용하면 API를 호출할 때 HTTP 헤더 &quot;Authorization&quot;의 일부로 XSTS 토큰을 전송할 수 있습니다. XSTS 토큰은 Primetime 유료 TV 인증에서 프로그래머에게 발급된 X.509 인증서의 공개 키를 사용하여 암호화해야 합니다. Primetime 유료 TV 인증은 연결된 개인 키를 저장하고 이를 사용하여 XSTS 토큰을 해독하고 해당 인증서에서 deviceId를 추출합니다.  


