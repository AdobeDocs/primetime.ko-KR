---
title: 사전 코드 변환 API
description: just-in-time repackaging API를 사용하여 광고 크리에이티브를 미리 코드 변환할 수 있으므로 콘텐츠 호환 버전은 필요할 때 사용할 수 있으며, JIT(Just-in-time) 리패키징과 관련된 2~4분 지연을 방지할 수 있습니다.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 사전 코드 변환 및 다시 패키징 API {#pre-transcoding-api}

Primetime Ad Insertion은 대형 직접 판매 이벤트처럼 크리에이티브 URL이 사전에 알려진 상황에 사전 코드 변환 API를 제공합니다.  이렇게 하면 정시 코드 변환과 관련된 2~4분 지연이 제거됩니다.

## HTTP 요청 {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

HTTP POST 명령을 지정된 URL로 전송하여 트랜스코딩할 광고 크리에이티브와 사용할 옵션을 CRS에 알려줍니다. 응답 코드는 성공 또는 실패 및 기타 정보를 보고합니다.

이 요청에는 사용자 이름과 암호가 필요합니다. Adobe 기술 계정 관리자에게 문의하십시오. 인증에 대한 정보가 필요한 경우 Adobe Primetime 지원 담당자에게 문의하십시오.

CRS에 트랜스코딩 요청을 제출하려면 다음과 같이 HTTP 메시지를 전송합니다.

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **방법 -** `POST`

* **인증 -** `Digest`

* **머리글 -** `Content-Type: text/xml`

* **본문 -** 다음 예제와 같은 XML

  ```xml
  <RepackageList>
      <Repackage>
          <AdSystem>Auditude</AdSystem>
          <AdID>AUD1</AdID>
          <CreativeID>AUD-CR1</CreativeID>
          <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
          <Zone>3</Zone>
      </Repackage>
      <Repackage>
          <AdSystem>Auditude</AdSystem>
          <AdID>AUD2</AdID>
          <CreativeID>AUD-CR1</CreativeID>
          <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
          <Format>id3 targetdur=5</Format>
          <Zone>3</Zone>
      </Repackage>
  </RepackageList>
  ```

다음 `RepackageList` 본문의 블록은 1에서 300까지 포함할 수 있습니다. `Repackage` 블록. 의 수인 경우 `Repackage` 본문의 블록이 300을 초과하면 다음 오류로 인해 HTTP 요청이 실패합니다.

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


의 필수 매개 변수와 선택적 매개 변수 `Repackage` 블록은 다음과 같습니다.

* **`AdSystem`** (필수) - 소스 광고 서버(예: ) `Auditude`, `FreeWheel`, `Apad.tv`. VAST 요소에 해당하는 문자열 값입니다. `AdSystem`.

* **`AdId`** (필수) - 요청에 지정된 타사 광고 서버에 대한 식별자입니다. 다음에 해당합니다. `id` 속성 `Ad` 요소를 VAST 응답에 추가합니다.

* **`CreativeURL`** (필수) - 트랜스코딩할 광고 크리에이티브의 위치(URI)입니다. 이는 VAST `MediaFile` 요소를 생성하지 않습니다.

* `CreativeID` (선택 사항) - 광고 경험의 일부로 포함될 광고 크리에이티브의 식별자입니다.
* **`Zone`** (필수) - 계정의 영역 ID입니다(기술 계정 관리자에게 문의). Auditude 플랫폼에 해당하는 숫자 값입니다 `publisher_site_id` 설정.

* **`Format`** (선택 사항) - CRS가 광고 문안을 변환하는 방법을 제어하는 매개 변수:

   * `clientside` - TVSDK가 CDN과 통신하는 데 사용하는 URL과 호환되는 출력을 생성합니다.

  >[!IMPORTANT]
  >
  >패키지된 광고가 클라이언트 측 Ad Insertion과 호환되도록 하려면 이 매개 변수를 제공해야 합니다. 이 기능을 제공하지 않으면 다시 패키징된 광고가 서버측 Ad Insertion과만 호환됩니다.

   * `hls` - HLS 호환 코드 변환 광고 크리에이티브를 생성합니다.
   * `dash` - DASH 호환 코드 변환 광고 크리에이티브를 생성합니다.
   * `id3` - ID3 시간 메타데이터 태그를 코드 변환된 광고 크리에이티브에 삽입합니다.
   * `targetdur` - 코드 변환된 광고 문안의 세그먼트 기간(초). 기본값은 입니다 `targetdur=4`. 이 값은 의 매니페스트에 지정된 값에 해당해야 합니다. `<s>` target 기간 태그에서: `#EXT-X-TARGETDURATION:<s>`.

  >[!NOTE]
  >
  >DASH 호환 에셋은 Adobe Primetime 광고 삽입과 호환되지 않습니다.

>[!IMPORTANT]
>
>가장 원활한 재생을 보장하려면 을 설정합니다. `targetdur` 콘텐츠 청크 지속 시간과 일치해야 합니다.

## HTTP 응답 {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS는 다음 상태 코드 중 하나로 요청에 응답합니다.

* **HTTP 202** - 수락됨(빈 본문 포함). 이는 성공을 나타냅니다. CRS는 트랜스코딩된 광고를 CDN 서버에 업로드합니다.
* **HTTP 400** - 잘못된 요청. 게시된 XML이 잘못되었습니다.
* **HTTP 500** - 내부 서버 오류. 서버에 내부 문제가 발생했습니다(예: 서버가 데이터베이스에 연결할 수 없음).

## SSAI 또는 CSAI용 사전 코드 변환 에셋 {#section_098888BB74FD4DC1AD0BD507B2A48318}

리패키징 API를 사용하여 향후 SSAI 또는 CSAI 이벤트를 사전 코딩할 수 있습니다. 자산이 향후에 SSAI와 함께 사용되도록 하려면 POST 호출의 모든 매개 변수가 고유한지 확인하십시오. 매개 변수는 AdSystem, AdId, CreativeURL, Zone, Format입니다. 이 매개변수 세트의 모든 차이는 SSAI에 대한 새로운 트랜스코딩 요청을 초래합니다.

향후 CSAI와 함께 사용되는 에셋의 경우 에셋의 고유성은 Zone 및 CreativeURL에 따라 달라집니다. AdSystem 및 AdId는 서로 다른 코드 변환된 자산을 생성하지 않으며 클라이언트에서 사용할 수 있습니다.
