---
description: Adobe Analytics 보고를 사용하도록 참조 구현을 설정할 수 있습니다.
title: Adobe Analytics 보고 구성
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Adobe Analytics 보고 구성 {#configure-adobe-analytics-reporting}

Adobe Analytics 보고를 사용하도록 참조 구현을 설정할 수 있습니다.

참조 구현은 Primetime SDK 내에 번들로 제공된 Adobe 모바일 라이브러리를 사용하여 Primetime 인증 이벤트 데이터를 Adobe Analytics에 보내도록 구성됩니다. 애플리케이션에서 전송된 이벤트 데이터를 활성화하고 사용하려면 먼저 Adobe Analytics 계정을 만들어야 합니다. 계정이 생성되면:

1. 계정 정보로 애플리케이션을 구성합니다.
1. 처리 규칙을 만들어 이벤트 데이터가 보고서 내에 표시되는 방법을 사용자 지정합니다.

아래 표에는 Adobe Analytics으로 전송된 데이터가 나와 있습니다.

| 작업 이름 | `a.media.pass.event.MvpdSelection` | 사용자가 선택 대화 상자에서 멀티채널 비디오 프로그래밍 배포자(MVPD)를 선택했습니다 |
|---|---|---|
| 컨텍스트 데이터 | `a.media.pass.MvpdId (String)` | 사용자가 선택한 MVPD |
|  | `a.media.pass.ClientType` | (문자열) 클라이언트 유형은 &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; 또는 &quot;android&quot;입니다. |
|  | | |
| 작업 이름 | `a.media.pass.event.AuthenticationDetection` | 인증 워크플로가 완료되었습니다. |
| 컨텍스트 데이터 | `a.media.pass.Successful` | (부울) 토큰 요청의 성공 여부, true 또는 false |
|  | `a.media.pass.MvpdId` | (문자열) 사용자가 선택한 MVPD입니다 |
|  | `a.media.pass.Guid` | (문자열) 추적 ID |
|  | `a.media.pass.Cached` | (부울) 토큰이 캐시에 이미 있습니다. true 또는 false |
|  | `a.media.pass.ClientType` | (문자열) 클라이언트 유형은 &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; 또는 &quot;android&quot;입니다. |
|  | | |
| 작업 이름 | `a.media.pass.event.AuthorizationDetection` | 인증 워크플로우가 완료되었습니다. |
| 컨텍스트 데이터 | `a.media.pass.Successful` | (부울) 토큰 요청의 성공 여부, true 또는 false |
|  | `a.media.pass.MvpdId` | (문자열) 사용자가 MVPD를 선택했습니다 |
|  | `a.media.pass.Guid` | (문자열) 추적 ID |
|  | `a.media.pass.Cached` | (부울) 토큰이 캐시에 이미 있습니다. true 또는 false |
|  | `a.media.pass.Error` | (문자열) 권한 부여 시도가 실패한 경우 오류 |
|  | `a.media.pass.ErrorDetails` | (문자열) 추가 오류 세부 정보 |
|  | `a.media.pass.ClientType` | (문자열) 클라이언트 유형은 &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; 또는 &quot;android&quot;입니다. |

1. Adobe Marketing Cloud에서 사용할 애플리케이션을 구성합니다.

   Primetime Primetime 인증 데이터를 Adobe Analytics에 보낼 수 있도록 하려면 [!DNL `ADBMobileConfig.json`] 컴파일 타임에 구성 파일을 참조 구현에 추가해야 합니다. 이는 Primetime SDK가 Video Analytics 데이터를 Marketing Cloud에게 보낼 때 사용한 것과 동일한 구성 파일입니다. 다음을 참조하십시오. [Adobe Marketing Cloud 설명서](https://microsite.omniture.com/t2/help/en_US/reference/) Adobe Analytics 계정으로 애플리케이션을 구성하는 방법에 대한 자세한 내용.
1. 처리 규칙을 만듭니다.

   참조 구현에서 전송한 Primetime 인증 이벤트 데이터는 분석 보고서에 자동으로 표시되지 않습니다. 먼저 처리 규칙을 만들어 데이터를 사용해야 합니다. 다음을 참조하십시오. [처리 규칙 만들기에 대한 Adobe Analytics 설명서](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
