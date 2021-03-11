---
description: Adobe Analytics 보고를 사용하도록 참조 구현을 설정할 수 있습니다.
title: Adobe Analytics 보고 구성
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# Adobe Analytics 보고 구성 {#configure-adobe-analytics-reporting}

Adobe Analytics 보고를 사용하도록 참조 구현을 설정할 수 있습니다.

참조 구현은 Primetime SDK에 번들로 제공되는 Adobe 모바일 라이브러리를 사용하여 Adobe Analytics에 Primetime 인증 이벤트 데이터를 전송하도록 구성되었습니다. 응용 프로그램에서 보낸 이벤트 데이터를 활성화하고 사용하려면 먼저 Adobe Analytics 계정을 만들어야 합니다. 계정을 만든 후:

1. 계정 정보로 응용 프로그램을 구성합니다.and
1. 처리 규칙을 만들어 보고서 내에서 이벤트 데이터가 표시되는 방식을 사용자 지정합니다.

아래 표는 Adobe Analytics으로 전송된 데이터를 보여줍니다.

| 작업 이름 | `a.media.pass.event.MvpdSelection` | 사용자가 선택 대화 상자에서 다중 채널 비디오 프로그래밍 디스트리러(MVPD)를 선택했습니다. |
|---|---|---|
| 컨텍스트 데이터 | `a.media.pass.MvpdId (String)` | 사용자가 선택한 MVPD |
|  | `a.media.pass.ClientType` | (문자열) 클라이언트 유형은 &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; 또는 &quot;android&quot;입니다. |
|  |  |  |
| 작업 이름 | `a.media.pass.event.AuthenticationDetection` | 인증 작업 과정이 완료되었습니다. |
| 컨텍스트 데이터 | `a.media.pass.Successful` | (부울) 토큰 요청이 성공했는지, true 또는 false인지 여부 |
|  | `a.media.pass.MvpdId` | (문자열) 사용자가 선택한 MVPD |
|  | `a.media.pass.Guid` | (문자열) 추적 ID |
|  | `a.media.pass.Cached` | (부울) 토큰이 이미 캐시에 있습니다. true 또는 false |
|  | `a.media.pass.ClientType` | (문자열) 클라이언트 유형은 &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; 또는 &quot;android&quot;입니다. |
|  |  |  |
| 작업 이름 | `a.media.pass.event.AuthorizationDetection` | 인증 작업 과정이 완료되었습니다. |
| 컨텍스트 데이터 | `a.media.pass.Successful` | (부울) 토큰 요청이 성공했는지, true 또는 false인지 여부 |
|  | `a.media.pass.MvpdId` | (문자열) 사용자가 선택한 MVPD |
|  | `a.media.pass.Guid` | (문자열) 추적 ID |
|  | `a.media.pass.Cached` | (부울) 토큰이 이미 캐시에 있습니다. true 또는 false |
|  | `a.media.pass.Error` | (문자열) 인증 시도가 실패한 경우 오류가 발생합니다. |
|  | `a.media.pass.ErrorDetails` | (문자열) 추가 오류 세부 정보 |
|  | `a.media.pass.ClientType` | (문자열) 클라이언트 유형은 &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; 또는 &quot;android&quot;입니다. |

1. Adobe Marketing Cloud에서 사용할 응용 프로그램을 구성합니다.

   Primetime Primetime 인증 데이터를 Adobe Analytics에 보내려면 컴파일 시 참조 구현에 [!DNL `ADBMobileConfig.json`] 구성 파일을 추가해야 합니다. 이는 Primetime SDK에서 Video Analytics 데이터를 Marketing Cloud에 전송하는 데 사용하는 구성 파일과 동일합니다. Adobe Analytics 계정으로 응용 프로그램을 구성하는 방법에 대한 자세한 내용은 [Adobe Marketing Cloud 설명서](https://microsite.omniture.com/t2/help/en_US/reference/)를 참조하십시오.
1. 처리 규칙을 만듭니다.

   참조 구현에서 보낸 Primetime 인증 이벤트 데이터는 분석 보고서에 자동으로 표시되지 않습니다. 먼저 처리 규칙을 만들어 데이터를 사용해야 합니다. 처리 규칙 만들기](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html)에 대한 자세한 내용은 [Adobe Analytics 설명서를 참조하십시오.
