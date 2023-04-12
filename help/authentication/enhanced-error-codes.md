---
title: 향상된 오류 코드
description: 향상된 오류 코드
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# 향상된 오류 코드 {#enhanced-error-codes}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요 {#overview}

이 문서에서는 API 오류 코드 목록과 애플리케이션에 다시 반환된 추가 오류 정보에 대해 설명합니다.

프로그래머 응용 프로그램에서 향상된 오류 코드를 사용하려면 구성 변경 시 지원 팀에 요청해야 합니다.

## 응답 오류 처리 {#response-error-handling}

대부분의 시나리오에서 Primetime 인증 API에는 제공을 위해 응답 본문에 추가 오류 정보가 포함됩니다 **의미 있는 컨텍스트** 특정 오류가 발생한 이유 및/또는 문제를 자동으로 해결할 수 있는 해결 방법을 알아봅니다.  *그러나 인증 또는 로그아웃 흐름과 관련된 일부 특정 경우에는 Primetime 인증 서비스가 HTML 응답 또는 빈 본문을 반환할 수 있습니다. 자세한 내용은 API 설명서를 참조하십시오.*

특정 유형의 오류는 자동으로 처리할 수 있지만(네트워크 시간 제한 시 인증 요청을 재시도하거나 세션이 만료된 경우 다시 인증해야 하는 경우 등), 다른 유형에는 구성 변경 또는 고객 지원 팀 상호 작용이 필요할 수 있습니다. 이러한 경우 프로그래머가 전체 오류 정보를 수집하고 제공하는 것이 중요합니다.

Primetime 인증 API는 오류 또는 오류를 나타내기 위해 400~500 범위의 HTTP 상태 코드를 반환합니다. 각 HTTP 상태 코드에는 다음과 같은 특정 영향이 있습니다.

- 4xx 오류 코드는 클라이언트가 오류를 생성하며 클라이언트가 오류를 해결하기 위해 추가 작업을 수행해야 함을 의미합니다(예: 보호된 API를 호출하거나 필요한 매개 변수를 제공하기 전에 액세스 토큰을 가져오는 경우)

- 5xx 오류 코드는 오류가 서버에서 생성되며 서버에서 오류를 해결하기 위해 추가 작업을 수행해야 함을 나타냅니다.

추가 오류 정보는 응답 본문의 &quot;오류&quot; 필드에 포함됩니다. 




| 이름 | 유형 | 예 | 설명 |
| --- | --- | --- | --- |
| **오류** | _개체_ | JSON <br>    {<br>        &quot;status&quot; : 403,<br>        &quot;code&quot; : &quot;network_connection_failure&quot;,<br>        &quot;message&quot; : &quot;TV 공급자 서비스에 연결할 수 없습니다.&quot;,<br>        &quot;helpUrl&quot; : &quot;&quot;,<br>        &quot;trace&quot; : &quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;action&quot; : &quot;retry&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | 요청을 완료하는 동안 수집된 컬렉션 또는 오류 개체입니다. |

</br>

여러 항목을 처리하는 Adobe Primetime API(사전 인증 API 등)는 특정 항목에 대해 처리가 실패했으며 항목 수준 오류 정보를 사용하여 다른 항목에 대해 성공적으로 수행되었는지 여부를 나타낼 수 있습니다. 이 경우 ***&quot;error&quot;*** 개체는 항목 수준에 있으며, 응답 본문에 여러 개가 있을 수 있습니다 ***&quot;errors&quot;*** 개체 - API 설명서를 참조하십시오.

</br>

| 부분 성공 및 항목 수준 오류가 있는 예 |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; : &quot;TestStream1&quot;,<br>  &quot;authorized&quot; : true <br>}, </br>{ </br>  &quot;id&quot; : &quot;TestStream2&quot;, <br>   &quot;authorized&quot; : false, </br>   &quot;error&quot; : { <br> </br>      &quot;status&quot; : 403,<br>      &quot;code&quot; : &quot;network_connection_failure&quot;,<br>      &quot;message&quot; : &quot;TV 공급자 서비스에 연결할 수 없습니다.&quot;,<br>      &quot;details&quot; : &quot;&quot;,<br>      &quot;helpUrl&quot; : &quot;&quot;,<br>      &quot;trace&quot; : &quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;action&quot; : &quot;retry&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

각 오류 객체에는 다음 매개 변수가 있습니다.

| 이름 | 유형 | 예 | 제한됨 | 설명 |
|----|----|----|----|--------------|
| 상태 | *정수* | 403 | ♦ | RFC 7231(https://tools.ietf.org/html/rfc7231#section-6)에 설명된 응답 HTTP 상태 코드 <br> - 400 잘못된 요청 <br> - 400 잘못된 요청 <br> - 400 잘못된 요청 <br> - 401 권한 없음 <br> - 403 금지됨 <br> - 404 찾을 수 없음 <br> - 405 메서드가 허용되지 않음 <br> - 409 충돌 <br> - 410 없어짐 <br> - 412 전제 조건 실패 <br> - 요청이 너무 많음 <br> - 500 간격 서버 오류 <br> - 503 서비스를 사용할 수 없음 |
| 코드 | *string* | network_connection_failure | ♦ | 표준 Primetime 인증 오류 코드입니다. 오류 코드의 전체 목록은 아래에 나와 있습니다. |
| 메시지 | *string* | TV 공급자 서비스에 연결할 수 없습니다. |  | 최종 사용자에게 표시할 수 있는 사람이 읽을 수 있는 메시지. |
| 세부 정보 | *string* | 구독 패키지에 &quot;라이브&quot; 채널이 포함되어 있지 않습니다 |  | 경우에 따라 MVPD 인증 종단점 또는 프로그램 관리자가 열화 규칙을 통해 자세한 메시지를 제공합니다. <br> <br> 파트너 서비스에서 사용자 지정 메시지를 받지 못한 경우 이 필드가 오류 필드에 없을 수 있습니다. |
| helpUrl | *url* | &quot;&quot; |  | 이 오류가 발생한 이유와 가능한 솔루션에 대한 자세한 정보를 연결하는 URL입니다. <br> <br>  URI는 절대 URL을 나타내며 오류 코드에서 추론해서는 안 됩니다. 오류 컨텍스트에 따라 다른 URL을 제공할 수 있습니다. 예를 들어 동일한 bad_request 오류 코드는 인증 및 인증 서비스에 대해 다른 url을 산출합니다. |
| trace | *string* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 |  | 보다 복잡한 시나리오에서 특정 문제를 식별하기 위해 지원에 문의할 때 사용할 수 있는 이 응답에 대한 고유 식별자입니다. |
| 작업 | *string* | 다시 시도 | ♦ | *상황을 해결하기 위한 권장 작업:* </br><br> -none - 안타깝게도 이 문제를 해결할 사전 정의된 작업이 없습니다. 이는 공용 API의 부적절한 호출을 나타낼 수 있습니다 </br><br>-configuration - TVE 대시보드를 통해 또는 지원 팀에 연락하여 구성을 변경해야 합니다. </br><br>-application-registration - 애플리케이션이 다시 등록해야 합니다. </br><br>-authentication - 사용자가 인증하거나 다시 인증해야 합니다. </br><br>-authorization - 사용자가 특정 리소스에 대한 권한을 받아야 합니다. </br><br>-degration - 어떤 형태의 열화를 적용해야 합니다. </br><br>-retry - 요청을 재시도하면 문제가 해결될 수 있습니다.</br><br>-retry-after - 표시된 기간이 문제를 해결할 수 있는 후 요청을 재시도합니다. |

</br>

**참고:**

- ***제한됨*** 열 *각 필드 값이 유한 집합을 나타내는지 여부를 나타냅니다.* (예: &quot;*상태*&quot; 필드)를 입력합니다. 이 사양에 대한 향후 업데이트에서는 제한된 목록에 값을 추가할 수 있지만 기존 값을 제거하거나 변경하지는 않습니다. 제한 없는 필드에는 일반적으로 데이터가 포함될 수 있지만, 적절한 크기를 유지하기 위해 제한이 있을 수 있습니다.

- 각 Adobe 응답에는 HTTP 서비스 전체에서 클라이언트 요청을 식별하는 &quot;Adobe-Request-Id&quot;가 포함됩니다. &quot;**trace**&#x200B;이 필드는 이 필드를 보완하며 함께 보고해야 합니다. 

## HTTP 상태 코드 및 오류 코드 {#http-status-codes-and-error-codes}

다양한 오류 코드와 연결된 HTTP 상태 코드 간의 불일치는 이전 sdk 및 애플리케이션과의 이전 호환성 요구 사항(예: *unknown\_application* 다음 기간 동안 400 잘못된 요청을 산출합니다. *unknown\_software\_statement* 401 권한 없음) 반환 이러한 불일치를 해결하는 것은 나중에 반복될 때 타깃팅됩니다. 
 
## 작업 및 오류 코드 {#actions-and-error-codes}

대부분의 오류 코드의 경우 문제를 직접 수정하는 경로로 여러 작업을 수행할 수 있거나 자동으로 수정하려면 여러 작업이 필요할 수 있습니다. 오류를 수정할 가능성이 가장 높은 항목을 표시하도록 선택했습니다. 다음 **작업** 는 다음 세 가지 카테고리로 분할할 수 있습니다.

1. 요청 컨텍스트를 수정하려고 하는 항목(다시 시도, 다시 시도) 
1. 애플리케이션 내에서 사용자 컨텍스트를 수정하려는 대상(애플리케이션 등록, 인증, 인증) 
1. 애플리케이션과 ID 공급자 간의 통합 컨텍스트를 수정하려고 하는 것(구성, 성능 저하)

첫 번째 카테고리(다시 시도 및 다시 시도 후)의 경우 동일한 요청을 재시도하면 문제를 해결할 수 있습니다. 여러 항목을 처리하는 API의 경우 애플리케이션에서 요청을 반복하고 &quot;다시 시도&quot; 또는 &quot;다시 시도 후&quot; 작업이 있는 항목만 포함해야 합니다. 에 대해&#x200B;*다시 시도 후*&quot; 작업, &quot;<u>다시 시도 후</u>&quot; 헤더는 애플리케이션이 요청을 반복하기 전에 대기해야 하는 시간(초)을 나타냅니다.

두 번째 및 세 번째 카테고리의 경우 실제 작업 구현은 애플리케이션 기능에 크게 의존합니다. 예: &quot;*분해*&quot; &quot;사용자가 컨텐츠를 재생할 수 있도록 15분 임시 패스로 전환&quot; 또는 &quot;지정된 MVPD와의 통합을 위해 AUTHN-ALL 또는 AUTHZ-ALL 저하를 적용할 자동 도구&quot;로 구현할 수 있습니다. 비슷함: &quot;*인증*&quot; 작업은 태블릿에서 수동 인증(백 채널 인증)을 트리거하고 연결된 TV에서 전체 2번째 화면 인증 흐름을 트리거할 수 있습니다. 스키마와 모든 매개 변수에 완벽한 URL을 제공하도록 선택한 이유입니다. 

## 오류 코드 {#error-codes}

아래 오류 표에는 가능한 오류 코드, 관련 메시지 및 가능한 작업이 나열되어 있습니다.

| 작업 | 오류 코드 | HTTP 상태 코드 | 설명 |
|---|---|---|--------------|
| 구성 | *authorization_denied_by_mvpd* | 403 | MVPD가 지정된 리소스에 대한 권한 부여를 요청할 때 &quot;거부&quot; 결정을 반환했습니다. |
|  | *authorization_denied_by_parent_controls* | 403 | MVPD가 지정된 리소스에 대한 자녀 보호 설정으로 인해 &quot;거부&quot; 결정을 반환했습니다. |
|  | *authorization_denied_by_programmer* | 403 | 프로그래머에서 적용한 저해 규칙은 현재 사용자에 대해 &quot;거부&quot; 결정을 적용합니다. |
|  | *bad_request* | 400 | API 요청이 잘못되었거나 잘못 구성되었습니다. API 설명서를 검토하여 요청 요구 사항을 결정합니다. |
|  | *personalization_service_unavailable* | 503 | 개인화 서비스를 사용할 수 없어 요청이 실패했습니다. |
|  | *internal_error* | 500 | 내부 서버 오류로 인해 요청에 실패했습니다. |
|  | *invalid_client_time* | 400 | 클라이언트 컴퓨터 날짜/시간/시간대가 올바르게 설정되지 않았습니다. 이로 인해 인증/인증 오류가 발생할 수 있습니다. |
|  | *invalid_custom_scheme* | 400 | 응용 프로그램 등록에 사용된 지정된 사용자 지정 체계를 인식할 수 없습니다. 적절한 사용자 지정 구성표 값에 대해서는 TVE 대시보드 구성을 확인하십시오. |
|  | *invalid_domain* | 400 | 요청자가 잘못된 도메인을 사용하고 있습니다. 특정 요청자 ID에서 사용하는 모든 도메인은 Adobe에서 화이트리스트에 추가해야 합니다. |
|  | *invalid_header* | 400 | 요청에 잘못된 헤더가 포함되어 있어서 이 요청에 실패했습니다. API 설명서를 검토하여 요청에 유효한 헤더와 해당 값에 대한 제한이 있는지 확인합니다. |
|  | *invalid_http_method* | 405 | 요청과 연결된 HTTP 메서드는 지원되지 않습니다. API 설명서를 검토하여 요청에 지원되는 HTTP 메서드를 확인합니다. |
|  | *invalid_parameter_value* | 400 | 요청에 잘못된 매개 변수 또는 매개 변수 값이 포함되어 있어서 요청이 실패했습니다. API 설명서를 검토하여 요청에 유효한 매개 변수와 값에 대한 제한 사항이 있는지 확인합니다. |
|  | *invalid_resource_value* | 400 | 잘못된 리소스 또는 잘못된 형식의 리소스를 사용하므로 요청이 실패했습니다. API 설명서를 검토하여 요청에 대해 얼마나 복잡한 리소스를 인코딩해야 하는지, 해당 값 및/또는 크기에 제한이 있는지 확인하십시오. |
|  | *invalid_registration_code | 404 | 지정한 등록 코드가 더 이상 유효하지 않거나 만료되었습니다. |
|  | *invalid_service_configuration* | 500 | 잘못된 서비스 구성으로 인해 요청이 실패했습니다. |
|  | *missing_authentication_header* | 400 | 특정 API에 필요한 인증 헤더가 포함되어 있지 않으므로 요청이 실패했습니다. |
|  | *missing_resource_mapping* | 400 | 지정한 리소스에 대한 해당 매핑이 없습니다. 필요한 매핑을 수정하려면 지원 센터에 문의하십시오. |
|  | *preauthorization_denied_by_mvpd* | 403 | MVPD가 지정된 리소스에 대한 사전 인증을 요청할 때 &quot;거부&quot; 결정을 반환했습니다. |
|  | *preauthorization_denied_by_programmer* | 403 | 프로그래머가 적용한 성능 저하 규칙은 현재 사용자에 대해 &quot;거부&quot; 결정을 적용합니다. |
|  | *registration_code_service_unavailable* | 503 | 등록 코드 서비스를 사용할 수 없으므로 요청이 실패했습니다. |
|  | *service_unavailable | 503 | 인증 또는 인증 서비스를 사용할 수 없다는 이유로 요청이 실패했습니다. |
|  | *access_token_unavailable* | 400 | 액세스 토큰을 검색하는 동안 예기치 않은 오류로 인해 요청이 실패했습니다. 사용 가능한 소프트웨어 구문 및 등록된 사용자 지정 구성표에 대해서는 TVE 대시보드 구성을 확인하십시오. |
|  | *unsupported_client_version* | 400 | 이 버전의 Primetime Authentication SDK는 너무 오래되어 더 이상 지원되지 않습니다. 최신 버전으로 업그레이드하는 데 필요한 단계는 API 설명서를 확인하십시오. |
|  | *network_required_ssl* | 403 | 대상 파트너 서비스에 대한 SSL 연결 문제가 있습니다. 지원 팀에 문의하십시오. |
|  | *too_many_resources* | 403 | 너무 많은 리소스를 쿼리하여 권한 부여 또는 사전 권한 부여 요청이 실패했습니다. 인증 및 사전 인증 제한을 제대로 구성하려면 지원 팀에 문의하십시오. |
|  | *unknown_programmer | 400 | 프로그래머 또는 서비스 공급자를 인식할 수 없습니다. TVE 대시보드를 사용하여 지정된 프로그래머를 등록합니다. |
|  | *unknown_application* | 400 | 응용 프로그램을 인식할 수 없습니다. TVE 대시보드를 사용하여 지정된 애플리케이션을 등록합니다. |
|  | *unknown_integration* | 400 | 지정한 프로그래머와 ID 공급자 간의 통합이 없습니다. TVE 대시보드를 사용하여 필요한 통합을 만듭니다. |
|  | *unknown_software_statement* | 401 | 액세스 토큰과 연결된 소프트웨어 문을 인식할 수 없습니다. 소프트웨어 문의 상태를 명확히 하려면 지원 팀에 문의하십시오. |
| 애플리케이션 등록 | *access_token_expired* | 401 | 액세스 토큰이 만료되었습니다. 애플리케이션은 API 설명서에 표시된 대로 액세스 토큰을 새로 고쳐야 합니다. |
|  | *invalid_access_token_signature* | 401 | 액세스 토큰 서명이 더 이상 유효하지 않습니다. 애플리케이션은 API 설명서에 표시된 대로 액세스 토큰을 새로 고쳐야 합니다. |
|  | *invalid_client_id* | 401 | 연결된 클라이언트 식별자를 인식할 수 없습니다. 애플리케이션은 API 설명서에 표시된 대로 애플리케이션 등록 프로세스를 따라야 합니다. |
| 인증 | *authentication_session_expired* | 410 | 현재 인증 세션이 만료되었습니다. 계속하려면 지원되는 MVPD로 다시 인증해야 합니다. |
|  | *authentication_session_missing* | 401 | 이 요청과 연결된 인증 세션을 검색할 수 없습니다. 계속하려면 지원되는 MVPD로 다시 인증해야 합니다. |
|  | *authentication_session_invalid* | 401 | ID 공급자가 인증 세션을 무효화했습니다. 계속하려면 지원되는 MVPD로 다시 인증해야 합니다. |
|  | *authentication_session_issuer_mismatch | 400 | 인증 흐름을 위한 표시된 MVPD가 인증 세션을 발행한 MVPD와 다른 것으로 인해 인증 요청이 실패했습니다. 계속하려면 원하는 MVPD로 다시 인증해야 합니다. |
|  | *authorization_denied_by_hba_policy* | 403 | MVPD가 홈 기반 인증 정책으로 인해 &quot;거부&quot; 결정을 반환했습니다. 홈 기반 인증 흐름(HBA)을 사용하여 현재 인증을 얻었지만 지정된 리소스에 대한 인증을 요청할 때 장치가 더 이상 작동하지 않습니다. 계속하려면 지원되는 MVPD로 다시 인증해야 합니다. |
|  | *identity_not_cognition_by_mvpd* | 403 | MVPD에서 사용자 ID를 인식하지 못하여 권한 부여 요청이 실패했습니다. |
| 권한 | *authorization_expired* | 410 | 지정한 리소스에 대한 이전 인증이 만료되었습니다. 계속하려면 사용자가 새 인증을 받아야 합니다. |
|  | *authorization_not_found* | 404 | 지정한 리소스에 대한 인증을 찾을 수 없습니다. 계속하려면 사용자가 새 인증을 받아야 합니다. |
|  | *device_identifier_mismatch* | 403 | 지정한 장치 식별자가 인증 장치 ID와 일치하지 않습니다. 계속하려면 사용자가 새 인증을 받아야 합니다. |
| 다시 시도 | **network_connection_failure** | 403 | 연결된 파트너 서비스에 연결하지 못했습니다. 요청을 재시도하면 문제가 해결될 수 있습니다. |
|  | *network_connection_timeout* | 403 | 연결된 파트너 서비스와의 연결 시간 제한이 있습니다. 요청을 재시도하면 문제가 해결될 수 있습니다. |
|  | *network_received_error* | 403 | 연결된 파트너 서비스에서 응답을 검색하는 동안 읽기 오류가 발생했습니다. 요청을 재시도하면 문제가 해결될 수 있습니다. |
|  | *maximum_execution_time_exceeded* | 403 | 최대 허용 시간 내에 요청이 완료되지 않았습니다. 요청을 재시도하면 문제가 해결될 수 있습니다. |
| 다시 시도 후 | *too_many_requests* | 429 | 지정된 간격 내에 너무 많은 요청이 전송되었습니다. 응용 프로그램은 제안된 기간 후에 요청을 다시 시도할 수 있습니다. |
|  | *user_rate_limit_exceeded* | 429 | 지정된 간격 내에 특정 사용자에 의해 너무 많은 요청이 발생했습니다. 응용 프로그램은 제안된 기간 후에 요청을 다시 시도할 수 있습니다. |

