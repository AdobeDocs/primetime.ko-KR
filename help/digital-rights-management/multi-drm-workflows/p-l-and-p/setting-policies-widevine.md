---
title: 출력 보호 정책 사용
description: 출력 보호 정책 사용
copied-description: true
exl-id: d91c9181-a6b2-4982-a3ba-57c4b56428eb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 출력 보호 정책 사용{#using-output-protection-policies}

**Widevine 출력 보호 정책**

Widevine은 기본적으로 아날로그 및 디지털 출력 보호 제한을 모두 지원합니다. 생성된 라이센스에 이러한 정책을 첨부하는 방법은 Widevine 서비스 공급자의 설명서를 참조하십시오.

Expressplay를 Widevine 서비스 공급자로 사용하는 경우 토큰 생성 시 hdcpOutputControl 플래그를 통해 디지털 출력 보호 정책을 연결합니다. 허용되는 값은 0, 1, 2이며, 여기서 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2입니다. HDCP_V1 및 HDCP_V2 모두 각각 HDCP 버전 1.X 및 2.X를 적용합니다.

Expressplay는 현재 아날로그 출력 제한 사항의 연결을 지원하지 않습니다.

**PlayReady 출력 보호 정책**

PlayReady는 기본적으로 아날로그 및 디지털 출력 보호 제한 사항을 모두 지원합니다. 설정할 수 있는 출력 보호 수준 값입니다. 페이지 [출력 보호 수준](https://msdn.microsoft.com/en-us/library/dn468831.aspx) 설정할 수 있는 값과 예상되는 클라이언트 동작을 설명합니다.

Expressplay를 사용하는 경우 compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL 및 unknownOutputBehavior 플래그를 통해 토큰 생성 시 출력 보호 수준 값을 첨부합니다. 문서화는에 제공됩니다. [PlayReady 라이선스 토큰 요청](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
