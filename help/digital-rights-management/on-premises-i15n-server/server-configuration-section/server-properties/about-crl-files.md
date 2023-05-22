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

제대로 작동하려면 개별화 및 라이센스 서버에 실행 중인 애플리케이션 서버(예: Tomcat)의 디스크에 캐시된 여러 CRL(인증서 해지 목록) 파일이 있어야 합니다. 새 CRL 파일은 정기적으로 디스크에 다운로드하고 캐시해야 합니다. 디스크에 있는 CRL 파일의 유효 기간이 경과할 수 있는 경우, 개별화 서버는 클라이언트의 개별화를 거부하고 라이센스 서버는 라이센스 발급을 거부합니다.

디스크에 캐시된 CRL에는 해당 URL과 일치하는 파일 이름이 있어야 합니다. 콜론 &#39;:&#39; 및 &#39;/&#39; 슬래시와 같은 특수 문자는 파일 이름에서 밑줄 &#39;_&#39;로 변환됩니다.

다음은 개별화 및 라이선스 서버 모두에서 사용되는 외부 호스팅 CRL 목록입니다.

* **중간 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 파일: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 유효성: 작성 후 약 12개월 동안 유효합니다.

* **루트 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 파일: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 유효성: 작성 후 약 5년 동안 유효합니다.

* **최신 CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 파일: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 유효성: 작성 후 약 3개월 동안 유효합니다.

라이센스 서버에서 사용할 수 있는 외부 호스팅 CRL에 대해 알아보려면 Adobe 지원 센터에 문의하십시오.

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

외부에서 호스팅된 CRL 외에도 추가 CRL을 생성하고 유지 관리할 수 있습니다. 다음에 지정된 대로 개별화 CA CRL입니다. [개별화 CA CRL 만들기](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 섹션에 있는 마지막 항목이 될 필요가 없습니다.

CRL은 만료되기 45일 전에 업데이트되도록 예약되어 있습니다. 이렇게 하면 인터넷에서 새로 생성된 CRL을 확보하고 설치할 수 있습니다. CRL 파일이 만료되기 전에 업데이트해야 합니다.
