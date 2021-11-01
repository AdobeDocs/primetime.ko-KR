---
title: CRL 파일 정보
description: CRL 파일 정보
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# CRL 파일 정보 {#about-crl-files}

제대로 작동하려면 개인 설정 및 라이선스 서버에서 실행 중인 응용 프로그램 서버(예: Tomcat)의 디스크에 여러 CRL(인증서 해지 목록) 파일을 캐시해야 합니다. 새 CRL 파일은 정기적으로 예약된 기준으로 디스크에 다운로드하여 캐시해야 합니다. 디스크에 있는 CRL 파일의 유효 기간이 경과하도록 허용되면 Personalization Server는 클라이언트를 개인화하는 것을 거부하며 라이센스 서버는 라이센스 발급을 거부합니다.

디스크에 캐시된 CRL에는 해당 URL과 일치하는 파일 이름이 있어야 합니다. 콜론 &#39;:&#39; 및 &#39;/&#39; 슬래시와 같은 특수 문자는 파일 이름에 밑줄 &#39;_&#39;로 변환됩니다.

다음은 개인화 및 라이센스 서버 모두에서 사용하는 외부에서 호스팅되는 CRL 목록입니다.

* **중간 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 파일: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 유효성: 생성 후 약 12개월 동안 유효합니다.

* **루트 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 파일: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 유효성: 창조 후 약 5년 동안 좋습니다

* **최신 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 파일: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 유효성: 생성 후 약 3개월 동안 유효합니다.

라이센스 서버에서 사용할 수 있는 외부에서 호스팅되는 CRL에 대해 알아보려면 Adobe 지원에 문의하십시오.

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

외부에서 호스팅되는 CRL 외에도 추가 CRL을 생성하고 관리할 수 있습니다. CA CRL은 [개인화 CA CRL 생성](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 섹션을 참조하십시오.

CRL은 만료되기 45일 전에 갱신될 예정입니다. 이렇게 하면 인터넷에서 새로 생성된 CRL을 획득하고 설치할 수 있는 충분한 시간이 필요합니다. CRL 파일이 만료되기 전에 업데이트해야 합니다.
