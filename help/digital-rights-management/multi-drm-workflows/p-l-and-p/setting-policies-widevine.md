---
title: 출력 보호 정책 사용
description: 출력 보호 정책 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# 출력 보호 정책 사용{#using-output-protection-policies}

**디바이스 출력 보호 정책**

기본적으로 Widevin은 아날로그 및 디지털 출력 보호 제한 사항을 모두 지원합니다. 생성된 라이센스에 이러한 정책을 첨부하는 방법에 대한 자세한 내용은 해당 무선 서비스 공급자의 설명서를 참조하십시오.

Express를 무선 서비스 공급자로 사용하는 경우 hdcpOutputControl 플래그를 통해 토큰 생성 시 디지털 출력 보호 정책을 첨부합니다.
허용되는 값은 0, 1, 2입니다. 여기서 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2입니다. HDCP_V1 및 HDCP_V2 모두 HDCP 버전 1.X 및 2.X를 적용합니다.

Express는 현재 아날로그 출력 제한 연결을 지원하지 않습니다.

**재생Ready 출력 보호 정책**

또한 PlayReady는 아날로그 및 디지털 출력 보호 제한 사항을 기본적으로 지원합니다. 설정할 수 있는 출력 보호 레벨 값입니다. [출력 보호 수준](https://msdn.microsoft.com/en-us/library/dn468831.aspx) 페이지는 설정할 수 있는 값과 예상되는 클라이언트 동작을 문서화합니다.

Express를 사용하는 경우 압축된DigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL 및 unknownOutputBehavior 플래그를 통해 토큰 생성 시간에 출력 보호 레벨 값을 첨부합니다. 이러한 내용은 [PlayReady 라이선스 토큰 요청](https://www.expressplay.com/developer/restapi/#playready-license-token-request)에 설명되어 있습니다.
