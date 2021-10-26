---
title: 보고서 API
description: Auditude 보고서 API
source-git-commit: 7f958c83a4dd481221feb4a266440b920ac7d195
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 보고서 API {#report-api}

사용자 인터페이스에는 고객 및 지원(Adobe) 팀을 위한 관리 역할이 있습니다. 고객은 포털에 액세스한 다음 해당 구성을 만들고 편집할 수 있습니다. 사용자 인터페이스에서 광고 노출 횟수에 대한 보고서를 볼 수도 있습니다.

API는 백엔드 인프라와 원활하게 의사 소통할 수 있도록 백그라운드에서 작동합니다.

## API 엔드포인트 {#report-api-endpoint}

### 프로덕션 {#production}

`https://dai-primetime.adobe.io/report`

### 샌드박스 {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## 쿼리 매개 변수


| 이름 | 유의 | 값 유형 | 필수? | 기본값 | 제한 | 예/유효한 샘플 값 |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | 보고서 데이터의 종료 날짜 | 날짜 | Y | 없음 | UTC-8에서 어제보다 최신 상태가 아님 | ######## |
| 필터 | 하나 이상의 열에 대해 필터링 | string | N | 없음 | ad_config_id , zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | 요청에서 metaData가 &#39;true&#39;로 설정된 경우 이름별로 필터링할 수도 있습니다. |  |
|  |  |  |  |  |  | 여러 필터 키는 세미콜론으로 구분됩니다. |
|  |  |  |  |  |  | 필터 키의 값 목록을 제공하려면 쉼표로 구분된 값을 사용하십시오 |
| groupBy | 시간(연도 \| 월 \| 일) 또는 ad_config_id로 그룹화합니다. Adconfig는 AdRule의 동의어입니다. | string | N | 없음 | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | groupBy의 경우 시간 내에 y 또는 m 또는 d 중 하나를 제공합니다. |
|  |  |  |  |  |  |  |



## 머리글 {#headers}

| 이름 | 값 유형 | 필수 | 샘플 값 | 유의 |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| 수락 | string | Y | CSV용 텍스트/csv | API에서 필요한 응답 유형 |
|  |  |  | application/json 또는 `*/* JSON용 &#39; |  |
| 인증 토큰 | string | Y | xyz | 인증 토큰 |
| x-api-key | string | Y | xyz | API 키 |
| x-gw-ims-org-id | string | Y | xyz12345 | 계정의 IMS 조직 ID |

* Adobe.io의 JWT 인증 도움말 페이지에 자세히 설명된 단계를 수행하여 인증 토큰(액세스 토큰이라고도 함)을 생성할 수 있습니다.
   >[!NOTE]
   >인증 토큰은 만료 24시간이므로 반복 스크립트를 사용하여 보고서 API를 사용하는 경우 만료 전에 인증 토큰을 생성하거나 토큰이 유효하지 않은 것에 대한 Oauth 오류가 발생했을 때 인증 토큰을 생성해야 합니다.

* 요청 헤더에서 올바른 값을 설정하고 인증 토큰(JWT 인증 사용)을 생성하려면 계정에 대해 아래 구성을 알고 있어야 합니다. Primetime 지원 팀에 문의하여 이러한 값을 받으십시오.
기술 계정 ID

   * 조직 ID
   * Api_key
   * Client_secret

## 출력 {#output}

Report API 쿼리의 결과는 기본적으로 요청된 차원(매개 변수별 그룹)의 다른 값에 대한 노출 횟수를 지정하는 JSON 형식입니다. 샘플 출력은 아래에 나와 있습니다.

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## 오류 코드 및 문자열 {#error-codes-strings}

### 오류 응답 형식 {#error-response-format}

매크로 &#39;code&#39;를 렌더링하는 동안 오류가 발생했습니다. 매개 변수에 대해 잘못된 값이 지정되었습니다. `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

아래 표에는 보고서 API에서 반환할 수 있는 오류 코드 및 메시지가 나와 있습니다. 인증 레이어와 관련된 오류는 다음을 참조하십시오. [오류 코드 설명서](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) Adobe.io

| 오류 코드 | 오류 메시지 |
|-----------------------|------------------------------------------|
| 4001007 | 사용자 세부 정보가 잘못되었습니다. |
| 4001008 | 모든 영역이 동일한 계정의 영역이 아닙니다. |
| 5001010 | 내부 오류가 발생했습니다. |
| 4001011 | 날짜는 필수 형식으로 전송되지 않습니다. |
| 4001012 | 날짜가 범위를 벗어났습니다. |
| 4001013 | 필수 매개 변수가 없습니다. |
| 4001014 | 계정의 영역 목록이 비어 있습니다. |
| 4001015 | 요청에 잘못된 필터 키가 있습니다. |
| 4001016 | 요청의 GroupBy 옵션이 잘못되었습니다. |
| 4001017 | 요청에 잘못된 ID가 제공되었습니다. |

## 샘플 호출 및 예상 결과 {#sample-calls-expected-results}

다음은 액세스 토큰을 사용하여 2020-07-01과 2021-06-30 사이의 월별 노출 횟수를 가져오는 curl 명령입니다.

**보고 API 호출 예**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| 샘플 호출/사용 사례 | 예상 결과 |
|---|---|
| 시작 및 종료 날짜가 있는 보고서 가져오기 GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 헤더 : Accept = application/json. 또는 */* | 이 account total_impressions에 속하는 모든 광고가 있는 다음 매개 변수가 있는 JSON |
| GroupBy = d \| m \| y GET을 사용하여 보고서 가져오기: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y 헤더 : Accept = application/json. 또는 */* | 이 계정 날짜(mm-dd-yyyy \| mm-yyyy \| yyyy 형식) total_impressions에 속하는 모든 광고가 있는 다음 매개 변수가 있는 JSON |
| GroupBy = ad_config_id GET을 사용하여 보고서 가져오기: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id 헤더 : Accept = application/json. 또는 */* | 이 계정 ad_config_id total_impressions에 속하는 모든 광고가 있는 다음 매개 변수가 있는 JSON |
| GroupBy = d \| m \| y 및 ad_config_id GET을 사용하여 보고서 가져오기: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id 헤더 : Accept = application/json. 또는 */* | 이 계정 ad_config_id 날짜(mm-dd-yyyy \| mm-yyyy \| yyyy 형식) total_impressions에 속하는 모든 광고가 있는 다음 매개 변수가 있는 JSON |
| metaData=true 및 groupBy=d \| m \| y GET을 사용하여 보고서 가져오기: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id 헤더 : Accept = application/json. 또는 */* | 이 계정 ad_config_id 이름 total_impressions에 속하는 모든 광고가 있는 다음 매개 변수가 있는 JSON |
| groupBy=d \| m \| y 및 ad_config_id GET을 사용하여 보고서 가져오기: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id 헤더 : Accept = application/json. 또는 */* | 이 계정 ad_config_id 이름 total_impressions 날짜(mm-dd-yyyy \| mm-yyyy \| yyyy 형식)에 속하는 모든 광고가 있는 다음 매개 변수가 있는 JSON입니다. |
| 보고서 가져오기 를 사용하여 지정된 날짜 범위에 대한 모든 행을 가져옵니다(페이지 없음 = true) GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 반환된 Json 배열의 31개 항목 |
| 유효한 페이지 쿼리 매개 변수를 사용하여 보고서 가져오기 GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 반환된 어레이의 5개 항목 |
| csv 형식 GET을 사용하여 보고서 가져오기: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 헤더 : 수락 = 텍스트/csv | CSV 문자열이 반환되고 헤더가 표시됩니다. total_impressions |
| csv 형식으로 보고서 가져오기 및 groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y 헤더 : 수락 = 텍스트/csv | CSV 문자열이 반환되고 헤더가 표시됩니다. total_impressions 날짜(mm-dd-yyyy \| mm-yyyy \| yyyy 형식) |
| csv 형식으로 보고서 가져오기 및 메타데이터 = true GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true header : 수락 = 텍스트/csv | CSV 문자열이 반환되고 헤더가 표시됩니다. total_impressions |
| csv 형식 , 메타데이터 = true 및 groupBy = d \| m \| y GET으로 보고서 가져오기: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y 헤더 : 수락 = 텍스트/csv | CSV 문자열이 반환되고 헤더가 표시됩니다. total_impressions 날짜(mm-dd-yyyy \| mm-yyyy \| yyyy 형식) |


## 보고서 API 제한 정책 {#report-api-throttling-policy}

* 5 API 요청은 각 사용자에 대해 5초 창 동안 허용됩니다.
* 사용자가 한도를 초과하는 경우 응답이 5초 지연됩니다.
* 사용자가 5초 이내에 10개 이상의 호출을 수행하면 응답 &quot;429 너무 많은 요청&quot;이 있는 거부됩니다.
