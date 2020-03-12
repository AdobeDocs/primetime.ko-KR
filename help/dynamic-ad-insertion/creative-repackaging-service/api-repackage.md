---
description: CRS 재패키징 API를 사용하여 비HLS 광고 크리에이티브를 미리 트랜스코딩할 수 있으므로 HLS 버전을 실행해야 할 때 사용할 수 있으므로 JIT(Just-In-Time) 재패키징과 관련된 2-4분 지연을 없앨 수 있습니다.
seo-description: CRS 재패키징 API를 사용하여 비HLS 광고 크리에이티브를 미리 트랜스코딩할 수 있으므로 HLS 버전을 실행해야 할 때 사용할 수 있으므로 JIT(Just-In-Time) 재패키징과 관련된 2-4분 지연을 없앨 수 있습니다.
seo-title: API 재패키징
title: API 재패키징
uuid: 03cd2428-510a-4b99-8496-059a48d5abba
translation-type: tm+mt
source-git-commit: 5c026bfc678bafc08f93ad056823e36fd77a8a25

---


# API 재패키징 {#repackaging-api}

CRS 재패키징 API를 사용하여 비HLS 광고 크리에이티브를 미리 트랜스코딩할 수 있으므로 HLS 버전을 실행해야 할 때 사용할 수 있으므로 JIT(Just-In-Time) 재패키징과 관련된 2-4분 지연을 없앨 수 있습니다.

## HTTP 요청 {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

HTTP POST 명령을 지정된 URL로 전송하여 트랜스코딩할 광고 크리에이티브와 이를 사용할 옵션을 CRS에 알려줍니다. 응답 코드는 성공 또는 실패 및 기타 정보를 보고합니다.

이 요청에는 사용자 이름과 암호가 필요합니다. Adobe 기술 계정 관리자에게 문의하십시오. 인증에 대한 정보가 필요한 경우 Adobe Primetime 지원 담당자에게 문의하십시오.

CRS에 트랜스코딩 요청을 제출하려면 다음과 같이 HTTP 메시지를 전송합니다.

* **URL -** https://id3.auditude.com/repackage [](https://id3.auditude.com/repackage)

* **메서드 -**`POST`

* **Auth -**`Digest`

* **머리글 -**`Content-Type: text/xml`

* **다음 예와 같이 본문** XML:

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

Body의 `RepackageList` 블록은 1-300 `Repackage` 블록을 포함할 수 있습니다. Body의 블록 수가 300개를 초과하는 `Repackage` 경우 다음 오류가 발생하여 HTTP 요청이 실패합니다.

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


블록에서 필수 매개 변수와 선택적 매개 변수는 다음과 같습니다. `Repackage`

* **`AdSystem`** (필수) - 소스 광고 서버(예: `Auditude`, `FreeWheel``Apad.tv`)입니다. VAST 요소에 해당하는 문자열 값입니다 `AdSystem`.

* **`AdId`** (필수) - 요청에 지정된 타사 광고 서버의 식별자입니다. VAST 응답에 있는 요소의 `id` 속성에 `Ad` 해당합니다.

* **`CreativeURL`** (필수) - 트랜스코딩할 광고 크리에이티브의 위치(URI)입니다. 이것은 VAST `MediaFile` 요소에 해당합니다.

* `CreativeID` (선택 사항) - 광고 경험의 일부로 포함할 광고 크리에이티브의 식별자입니다.
* **`Zone`** (필수) - 계정의 영역 ID(기술 계정 관리자의 확인). 이것은 Auditude 플랫폼 `publisher_site_id` 설정에 해당하는 숫자 값입니다.

* **`Format`** (선택 사항) - CRS가 광고 크리에이티브를 트랜스코딩하는 방법을 제어하는 매개 변수:

   * `clientside` - TVSDK가 CDN과 통신하는 데 사용하는 URL과 호환되는 출력을 생성합니다.
   >[!IMPORTANT]
   >
   >다시 패키지된 광고가 클라이언트측 광고 삽입과 호환되도록 하려면 이 매개 변수를 제공해야 합니다. 이 기능을 제공하지 않으면 다시 패키지된 광고는 서버측 광고 삽입과 호환됩니다.

   * `hls` - HLS 호환 트랜스코딩 광고 크리에이티브를 생성합니다.
   * `dash` - DASH 호환 트랜스코딩된 광고 크리에이티브를 생성합니다.
   * `id3` - ID3 시간 지정 메타데이터 태그를 코드 변환된 광고 크리에이티브에 삽입합니다.
   * `targetdur` - 코드 변환된 광고 크리에이티브의 세그먼트 기간(초)입니다. 기본값은 `targetdur=4`입니다. 이 값은 대상 기간 태그에 대해 매니페스트에 지정된 `<s>` 값에 해당해야 합니다. `#EXT-X-TARGETDURATION:<s>`Adobe
   >[!NOTE]
   >
   >DASH 호환 에셋은 Adobe Primetime 광고 삽입과 호환되지 않습니다.

>[!IMPORTANT]
>
>매끄러운 재생을 보장하려면 컨텐츠 청크 지속 시간과 일치하도록 `targetdur` 설정합니다.

## HTTP 응답 {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS는 다음 상태 코드 중 하나로 요청에 응답합니다.

* **HTTP 202** - 허용됨(빈 본문 포함). 성공을 나타냅니다. CRS는 트랜스코딩된 광고를 CDN 서버에 업로드합니다.
* **HTTP 400** - 잘못된 요청입니다. 게시된 XML이 잘못되었습니다.
* **HTTP 500** - 내부 서버 오류입니다. 서버에 내부 문제가 발생했습니다(예: 서버에 데이터베이스에 연결할 수 없음).

## SSAI 또는 CSAI용 사전 트랜스코딩 에셋 {#section_098888BB74FD4DC1AD0BD507B2A48318}

재패키징 API를 사용하면 향후 SSSAI 또는 CSAI 이벤트를 사전에 트랜스코딩할 수 있습니다. 향후 자산이 SAI와 함께 사용되도록 하려면 POST 호출의 모든 매개 변수가 고유해야 합니다. 매개 변수는 다음과 같습니다.AdSystem, AdId, CreativeURL, Zone, Format. 이 매개 변수 세트의 차이점이 있으면 SSSAI에 대한 새로운 트랜스코딩 요청이 발생합니다.

나중에 CSAI와 함께 사용되는 자산의 경우 자산 고유성은 Zone 및 CreativeURL에 따라 달라집니다. AdSystem 및 AdId는 서로 다른 코드 변환된 에셋으로 연결되지 않으며 클라이언트에서 이를 사용할 수 있습니다.
