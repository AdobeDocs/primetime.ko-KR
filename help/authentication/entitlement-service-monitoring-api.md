---
title: 자격 부여 서비스 모니터링 API
description: 자격 부여 서비스 모니터링 API
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 0%

---


# 자격 부여 서비스 모니터링 API {#entitlement-service-monitoring-api}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## API 개요 {#api-overview}

자격 부여 서비스 모니터링(ESM)은 WOLAP(웹 기반)로 구현됩니다 [온라인 분석 처리](https://en.wikipedia.org/wiki/Online_analytical_processing){target=_blank}) 프로젝트를 만들 수 있습니다. ESM은 데이터 웨어하우스에서 지원하는 일반 비즈니스 보고 웹 API입니다. 일반 OLAP 작업을 RESTfully로 수행할 수 있도록 해주는 HTTP 쿼리 언어로서 작동합니다.

>[!NOTE]
>
>ESM API는 일반적으로 사용할 수 없습니다. 가용성에 대한 질문이 있으면 Adobe 담당자에게 문의하십시오.

ESM API는 기본 OLAP 큐브의 계층적 뷰를 제공합니다. 각 리소스([차원](#esm_dimensions) 차원 계층 구조에서 URL 경로 세그먼트로 매핑되는)은 (집계됨)이 있는 보고서를 생성합니다 [지표](#esm_metrics) 을 선택합니다. 각 리소스는 상위 리소스(롤업용) 및 하위 리소스(드릴다운용)를 가리킵니다. 차원을 특정 값 또는 범위에 고정하는 쿼리 문자열 매개 변수를 통해 슬라이싱 및 사전이 수행됩니다.

REST API는 차원 경로, 제공된 필터 및 선택한 지표에 따라 요청에 지정된 시간 간격(제공된 데이터가 없는 경우 기본값으로 폴백) 내에서 사용 가능한 데이터를 제공합니다. 시간 차원(연도, 월, 일, 시간, 분, 초)이 포함되지 않은 보고서에는 시간 범위가 적용되지 않습니다.

끝점 URL 루트 경로는 사용 가능한 드릴다운 옵션에 대한 링크와 함께 단일 레코드 내에 있는 전체 집계된 지표를 반환합니다. API 버전이 끝점 URI 경로의 후행 세그먼트로 매핑됩니다. 예, `https://mgmt.auth.adobe.com/*v2*` 은 클라이언트가 WOLAP 버전 2에 액세스함을 의미합니다.

사용 가능한 URL 경로는 응답에 포함된 링크를 통해 검색할 수 있습니다. 유효한 URL 경로는 집계된 (사전) 지표를 포함하는 기본 드릴다운 트리 내에 경로를 매핑하기 위해 유지됩니다. 양식의 패스 `/dimension1/dimension2/dimension3` 는 이러한 세 차원의 사전 합계를 반영합니다(SQL과 같음). `clause GROUP` 기준 `dimension1`, `dimension2`, `dimension3`). 이러한 사전 집계가 존재하지 않고 시스템에서 즉시 이를 계산할 수 없는 경우 API는 404 찾을 수 없음 응답을 반환합니다.

## 드릴 다운 트리 {#drill-down-tree}

다음 드릴다운 트리는 ESM 2.0에서 사용할 수 있는 차원(리소스)을 보여줍니다. [프로그래머] (#esm_dimensions) 및 [MVPD](#esm_dimensions_mvpd).


### 프로그래머가 사용할 수 있는 Dimension {#progr-dimensions}

![](assets/esm-progr-dimensions.png)

### MVPD에서 사용할 수 있는 Dimension {#mvpd-dimensions}

![](assets/esm-mvpd-dimensions.png)

에 대한 GET `https://mgmt.auth.adobe.com/v2` API 종단점은 다음을 포함하는 표현을 반환합니다.

* 사용 가능한 루트 드릴다운 경로에 대한 링크:

   * `<link rel="drill-down" href="/v2/dimensionA"/>`

   * `<link rel="drill-down" href="/v2/dimensionB"/>`

* 모든 지표에 대한 요약(집계된 값)입니다(쿼리 문자열 매개 변수가 제공되지 않았으므로 기본 간격에서).


드릴다운 경로(단계별)에 따라 다음을 수행합니다.
`/dimensionA/year/month/day/dimensionX` 는 다음 응답을 검색합니다.

* 링크:`dimensionY`&quot; 및 &quot;`dimensionZ`&quot; 드릴다운 옵션

* 각 값에 대한 일별 합계를 포함하는 보고서 `dimensionX`


### 필터

날짜/시간 차원을 제외하고 현재 투영(차원 경로)에 사용할 수 있는 모든 차원은 쿼리 문자열 매개 변수로 해당 이름을 사용하여 필터링할 수 있습니다.

다음 필터링 옵션을 사용할 수 있습니다.

* **다음과 같음** 필터는 쿼리 문자열에서 차원 이름을 특정 값으로 설정하여 제공됩니다.

* **IN** 동일한 차원 이름 매개 변수를 다른 값으로 여러 번 추가하여 필터를 지정할 수 있습니다. dimension=value1\&amp;dimension=value2

* **같지 않음** 필터는 &#39;\!&#39;를 사용해야 합니다. 차원 이름 뒤에 &#39;\!=&#39; &quot;operator&quot;: dimension\!= 값

* **NOT IN** 필터에 &#39;\!=&#39; 연산자를 여러 번 사용할 수 있습니다. dimension\!= value1\&amp;dimension\!= 값2&amp;...

쿼리 문자열에서 차원 이름에 대한 특수 용도가 있습니다. 차원 이름이 값이 없는 쿼리 문자열 매개 변수로 사용되는 경우 API에 해당 차원을 포함하는 투영을 보고서에 반환하도록 지시합니다.

### ESM 쿼리 예

| *URL* | *SQL 동등 항목* |
|---|---|
| /dimension1/dimension2/dimension3?dimension1=value1 | 투영 WHERE dimension1 = &#39;value1&#39;에서 *를 선택합니다. </br> 그룹화 기준 차원1, 차원2, 차원3 |
| /dimension1/dimension2/dimension3?dimension1=value1&amp;dimension1=value2 | 투영 WHERE dimension1 IN(&#39;value1&#39;, &#39;value2&#39;)에서 *를 선택합니다. </br> 그룹화 기준 차원1, 차원2, 차원3 |
| /dimension1/dimension2/dimension3?dimension1!=value1 | 투영 WHERE dimension1 &lt;> &#39;value1&#39;에서 *를 선택합니다. | </br> 그룹화 기준 차원1, 차원2, 차원3 |
| /dimension1/dimension2/dimension3?dimension1!= value1&amp;dimension2!=value2 | 투영 WHERE dimension1이 NOT IN(&#39;value1&#39;, &#39;value2&#39;)에서 *를 선택합니다. | </br> 그룹화 기준 차원1, 차원2, 차원3 |
| 직접 경로가 없다고 가정할 경우: /dimension1/dimension3 </br> 하지만 경로가 있습니다. /dimension1/dimension2/dimension3 </br> </br> /dimension1?dimension3 | 투영 GROUP BY dimension1, dimension3에서 *를 선택합니다. |

>[!NOTE]
>
>이러한 필터링 기법은 어느 것에도 작동하지 않습니다 `date/time` 차원. 필터링 방법 `date/time` 차원은 `start` 및 `end` 쿼리 문자열 매개 변수(아래에 설명)가 필요한 값에 적용됩니다.

다음 쿼리 문자열 매개 변수는 API에 대해 예약된 의미가 있으므로 차원 이름으로 사용할 수 없거나 이러한 차원에 대해 필터링을 수행할 수 없습니다.

### ESM API 예약된 쿼리 문자열 매개 변수

| 매개 변수 | 선택 사항입니다 | 설명 | 기본값 | 예 |
| --- | ---- | --- | ---- | --- |
| access_token | 예 | IMS OAuth 보호가 활성화된 경우 IMS 토큰을 표준 인증 베어러 토큰 또는 쿼리 문자열 매개 변수로 전달할 수 있습니다. | 없음 | access_token=XXXXXX |
| dimension-name | 예 | 모든 차원 이름 - 현재 URL 경로나 유효한 하위 경로에 포함되어 있습니다. 값은 다음과 같은 필터로 처리됩니다. 값을 제공하지 않으면 지정된 차원이 포함되지 않았거나 현재 경로에 인접한 경우에도 출력에 포함됩니다 | 없음 | someDimension=someValue&amp;someOtherDimension |
| end | 예 | 보고서 종료 시간(밀리초 단위) | 서버의 현재 시간 | end=2012-07-30 |
| 포맷 | 예 | 컨텐츠 협상에 사용됩니다(효과가 동일하지만 &quot;확장&quot; 경로보다 우선순위가 낮은 경우 - 아래 참조). | 없음: 콘텐츠 협상은 다른 전략을 시도할 것이다 | format=json |
| 제한 | 예 | 반환할 최대 행 수 | 요청에 제한이 지정되지 않은 경우 자체 링크에서 서버가 보고한 기본값 | limit=1500 |
| 지표 | 예 | 반환할 지표 이름의 쉼표로 구분된 목록; 이 값은 사용 가능한 지표의 하위 집합을 필터링하고(페이로드 크기를 줄이기 위해) API를 적용하여 요청된 지표(기본 최적 투영 대신)가 포함된 투영을 반환하는 데에도 사용해야 합니다. | 이 매개 변수가 제공되지 않을 경우 현재 투영에 사용할 수 있는 모든 지표가 반환됩니다. | metrics=m1,m2 |
| start | 예 | 보고서 시작 시간(ISO8601) 접두사만 제공되면 서버가 나머지 부품을 입력합니다. 예: start=2012를 입력하면 start=2012-01-01:00:00:00 | 서버가 자체 링크에서 보고한 경우 서버는 선택한 시간 세부기간을 기반으로 적절한 기본값을 제공하려고 합니다 | start=2012-07-15 |

현재 사용할 수 있는 유일한 HTTP 메서드는 GET입니다. OPTIONS/HEAD 방법에 대한 지원은 향후 버전에서 제공될 수 있습니다.

## ESM API 상태 코드 {#esm-api-status-codes}

| 상태 코드 | 원인 구 | 설명 |
|---|---|---|
| 200 | 확인 | 응답에는 &quot;롤업&quot; 및 &quot;드릴다운&quot; 링크(해당되는 경우)가 포함됩니다. 보고서가 리소스의 특성으로 렌더링됩니다. 중첩된 &quot;보고서&quot; 요소/속성입니다. |
| 400 | 잘못된 요청 | 응답 본문에는 요청의 문제를 설명하는 텍스트 메시지가 포함됩니다. </br> </br> 400 잘못된 요청 상태는 클라이언트 오류에 대한 유용한 정보를 제공하는 응답 본문(일반/텍스트 미디어 유형)에 설명 텍스트와 함께 제공됩니다. 유효하지 않은 날짜 형식 또는 비기존 차원에 적용된 필터와 같은 간단한 시나리오 외에도, 시스템에서는 대량의 데이터가 즉시 반환되거나 집계되어야 하는 쿼리에 응답하기를 거부합니다. |
| 401 | 권한 없음 | 사용자를 인증하기 위해 적절한 OAuth 헤더를 포함하지 않는 요청으로 인해 발생합니다 |
| 403 | 금지됨 | 현재 보안 컨텍스트에서 요청이 허용되지 않음을 나타냅니다; 이 문제는 사용자가 인증되었지만 요청된 정보에 액세스할 수 없는 경우에 발생합니다 |
| 404 | 없음 | 잘못된 URL 경로가 요청과 함께 제공되는 경우 이 발생합니다. 클라이언트가 200개의 응답이 있는 &quot;drill-down&quot;/&quot;roll-up&quot; 링크를 따르는 경우에는 이러한 문제가 발생하지 않습니다 |
| 405 | 메서드가 허용되지 않음 | 요청에서 지원되지 않는 방법이 사용되었음을 나타냅니다. 현재는 GET 메서드만 지원되지만, 향후 버전에서는 HEAD 또는 OPTIONS이 허용됩니다 |
| 406 | 허용되지 않음 | 클라이언트가 지원되지 않는 미디어 유형을 요청했음을 나타냅니다. |
| 500 | 내부 서버 오류 | &quot;이런 일은 절대 일어나지 말아야 한다&quot; |
| 503 | 서비스를 사용할 수 없음 | 응용 프로그램 또는 해당 종속성 내에 오류를 신호합니다 |

## 데이터 형식 {#data-formats}

데이터는 다음 형식으로 사용할 수 있습니다.

* JSON(기본값)
* XML
* CSV
* HTML(데모 목적)

클라이언트는 다음 컨텐츠 협상 전략을 사용할 수 있습니다(우선 순위는 목록의 위치에 의해 지정됨 - 우선 순위).

1. URL 경로의 마지막 세그먼트에 추가된 &quot;파일 확장명&quot;입니다. 예, `/esm/v2/media-company/year/month/day.xml`. URL에 쿼리 문자열이 들어 있는 경우 확장 프로그램이 물음표 앞에 와야 합니다. `/esm/v2/media-company/year/month/day.csv?mvpd= SomeMVPD`
1. 형식 쿼리 문자열 매개 변수: 예, `/esm/report?format=json`
1. 표준 HTTP Accept 헤더: 예, `Accept: application/xml`

확장 및 쿼리 매개 변수 모두 다음 값을 지원합니다.

* xml
* json
* csv
* html

전략에서 지정한 미디어 유형이 없는 경우, API는 기본적으로 JSON 컨텐츠를 생성합니다.

## 하이퍼텍스트 응용 프로그램 언어 {#hypertext-application-language}

JSON 및 XML의 경우 페이로드가 여기에 설명된 대로 HAL로 인코딩됩니다.  <http://stateless.co/hal_specification.html>.

실제 보고서(중첩된 태그/속성 &quot;보고서&quot;라고 함)는 다음과 같이 인코딩된 상태로 선택한/적용 가능한 모든 차원 및 지표를 포함하는 실제 레코드 목록으로 구성됩니다.

### JSON

```JSON
 "report": [
  {
    "dimension1": "d1",
    ...
    "metric1": "m1",
    ...
  }, {
    ...
  }
]
```

### XML

```XML
 <report>
  <record dimension1="d1" ... metric1="m1" ... />
  ...
</report
```

XML 및 JSON 형식의 경우 레코드 내의 필드(차원 및 지표) 순서는 지정되지 않지만 일관됩니다(순서는 모든 레코드에서 동일함). 그러나 클라이언트는 레코드 내의 특정 필드 순서에 의존하지 않아야 합니다.

리소스 링크(JSON의 &quot;self&quot; rel 및 XML의 &quot;href&quot; 리소스 속성)에는 인라인 보고서에 사용되는 현재 경로와 쿼리 문자열이 포함되어 있습니다. 쿼리 문자열은 암시적 및 명시적 매개 변수를 모두 표시하므로 페이로드가 사용되는 시간 간격, 암시적 필터(있는 경우) 등을 명시적으로 가리키도록 합니다. 리소스 내의 나머지 링크에는 현재 데이터로 드릴다운하기 위해 따를 수 있는 모든 사용 가능한 세그먼트가 포함됩니다. 롤업용 링크도 제공되며, 상위 경로(있는 경우)를 가리킵니다. 다음 `href` 드릴다운/롤업 링크의 값은 URL 경로만 포함합니다(쿼리 문자열은 포함되지 않으므로 필요한 경우 클라이언트가 이 경로를 추가해야 합니다.). 현재 리소스에 사용된(또는 암시적) 쿼리 문자열 매개 변수 중 일부가 &quot;롤업&quot; 또는 &quot;드릴다운&quot; 링크에 적용되지 않습니다(예: 필터는 하위 또는 상위 리소스에 적용되지 않을 수 있음).

예(다음의 단일 지표가 있다고 가정함) `clients` 및에 대한 사전 집계가 있습니다. `year/month/day/...`):

* https://mgmt.auth.adobe.com/esm/v2/year/month.xml

```XML
   <resource href="/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21">
   <links>
   <link rel="roll-up" href="/esm/v2/year"/>
   <link rel="drill-down" href="/esm/v2/year/month/day"/>
   </links>
   <report>
   <record month="6" year="2012" clients="205"/>
   <record month="7" year="2012" clients="466"/>
   </report>
   </resource>
```

* https://mgmt.auth.adobe.com/esm/v2/year/month.json 

   ```JSON
       {
         "_links" : {
           "self" : {
             "href" : "/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21"
           },
           "roll-up" : {
             "href" : "/esm/v2/year"
           },
           "drill-down" : {
             "href" : "/esm/v2/year/month/day"
           }
         },
         "report" : [ {
           "month" : "6",
           "year" : "2012",
           "clients" : "205"
         }, {
           "month" : "7",
           "year" : "2012",
           "clients" : "466"
         } ]
       }
   ```

### CSV

CSV 데이터 형식에서는 링크 또는 기타 메타데이터(헤더 행 제외)가 인라인으로 제공되지 않습니다. 대신 선택 메타데이터가 파일 이름에 제공되어 다음 패턴을 따릅니다.

```CSV
    esm__<start-date>_<end-date>_<filter-values,...>.csv
```

CSV에는 머리글 행이 포함된 다음 보고서 데이터를 후속 행으로 포함합니다. 헤더 행에는 모든 차원 뒤에 모든 지표가 옵니다. 보고서 데이터의 정렬 순서는 차원 순서에 반영됩니다. 따라서 데이터가 `D1` 다음에 `D2`로 지정하는 경우 CSV 헤더는 다음과 같습니다. `D1, D2, ...metrics...`.

헤더 행의 필드 순서는 테이블 데이터의 정렬 순서를 반영합니다.


예: https://mgmt.auth.adobe.com/v2/year/month.csv에서 라는 파일을 생성합니다 `report__2012-07-20_2012-08-20_1000.csv` 다음 컨텐츠와 함께 사용할 수 있습니다.


| 년 | 월 | 클라이언트 |
| ---- | :---: | ------- |
| 2012 | 6 | 580 |
| 2012 | 7 | 231 |

## 데이터 새로 고침 {#data-freshness}

성공적인 HTTP 응답에는 `Last-Modified` 머리글: 본문에서 보고서를 마지막으로 업데이트한 시간을 나타냅니다. 마지막 수정 날짜 헤더의 부족은 보고서 데이터가 실시간으로 계산됨을 나타냅니다.

일반적으로 조그된 데이터는 세분화된 데이터(예: 분 값 또는 시간별 값)보다 덜 자주 업데이트됩니다. 특히 고유한 카운트와 같이 작은 세부기간을 기준으로 계산할 수 없는 지표의 경우 일별 값보다 최신이 될 수 있습니다.

향후 버전의 ESM에서는 클라이언트가 표준 &quot;If-Modified-Since&quot; 헤더를 제공하여 조건부 GET을 수행할 수 있습니다.

## GZIP 압축 {#gzip-compression}

Adobe은 ESM 보고서를 가져오는 클라이언트에서 gzip 지원을 사용하도록 설정하는 것이 좋습니다. 이렇게 하면 응답 크기가 크게 줄어들어 응답 시간이 줄어듭니다. (ESM 데이터의 압축률은 20-30 범위에 있습니다.)

클라이언트에서 gzip 압축을 활성화하려면 `Accept-Encoding:` 헤더:

* 수락 인코딩: gzip, deflate


<!--
## Related Information {#related-information}

- [ESM Overview](/help/authentication/entitlement-service-monitoring-overview.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Understanding Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->