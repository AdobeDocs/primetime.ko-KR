---
seo-title: CRL 파일 정보
title: CRL 파일 정보
uuid: 672c3ca0-5c5d-4ec7-83b1-f0f8e34c8d09
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# CRL 파일 정보 {#about-crl-files}

Individuation and License Server가 제대로 작동하려면 실행 중인 응용 프로그램 서버(예: Tomcat)의 디스크에 여러 CRL(Certificate Revocation List) 파일이 캐시되어야 합니다. 새로운 CRL 파일은 정기적으로 예약된 방식으로 다운로드하여 디스크에 캐시해야 합니다. 디스크에 있는 CRL 파일의 유효 기간이 만료될 경우 Indistration Server는 클라이언트를 개인 식별하지 않으며 라이센스 서버는 라이센스 발급을 거부합니다.

디스크에 캐시된 CRL에는 해당 URL과 일치하는 파일 이름이 있어야 합니다. 콜론 &#39;:&#39; 및 &#39;/&#39; 슬래시와 같은 특수 문자는 파일 이름에서 밑줄 &#39;_&#39;로 변환됩니다.

다음은 개인화 및 라이센스 서버 모두에서 사용되는 외부에서 호스트된 CRL 목록입니다.

* **중간 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 파일: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 유효성:제작 후 약 12개월 동안 적합

* **루트 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 파일: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 유효성:창작 후 약 5년 동안 사용 가능

* **최신 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 파일: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 유효성:제작 후 약 3개월 동안 적합

다음은 라이센스 서버에서만 사용되는 외부에서 호스트된 CRL입니다.

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* 파일: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* 유효성:제작 후 약 3개월 동안 적합

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* 파일: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* 유효성:제작 후 약 3개월 동안 적합

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* 파일: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* 유효성:제작 후 약 3개월 동안 적합

앞서 언급한 CRL 외에도 추가 CRL을 만들고 유지 관리해야 합니다. 이 문서의 개인화 CA CRL 만들기 [섹션에 지정된 개인화](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) CA CRL입니다.

CRL은 만료되기 45일 전에 업데이트될 예정입니다. 이렇게 하면 인터넷에서 새로 생성된 CRL을 확보하고 설치할 수 있는 충분한 시간이 필요합니다. CRL 파일이 만료되기 전에 업데이트해야 합니다.
