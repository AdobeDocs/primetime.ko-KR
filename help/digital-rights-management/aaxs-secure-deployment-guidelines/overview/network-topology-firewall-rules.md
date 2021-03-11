---
title: 방화벽 규칙
description: 방화벽 규칙
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# 방화벽 규칙 {#firewall-rules}

## 들어오는 URL {#section-F111526A9DB844CBBF21A3CAE5F50880}

최종 사용자에게 제공하려는 응용 프로그램 기능에 대한 URL만 표시되도록 외부 방화벽을 구성합니다. 외부 사용자가 외부 방화벽을 통해 다음 표에 나열된 URL에만 액세스할 수 있도록 허용:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-bqs-whz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">루트 URL </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">목적 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/getServerVersion/v3</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">서버 버전을 확인하는 URL입니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-xr4-hdn-44"> 
     <li id="li-05925A4DE4114F7786FF93A66AB8A117"><span class="filepath"> /flashaccess/authn/v1/*</span> </li> 
     <li id="li-E76E9BA0160F4E7F9EBB64428C2D9F31"><span class="filepath"> /flashaccess/authn/v3/*</span> </li> 
     <li id="li-ED3C15EB4D194FFE99954BDB7D5C1E41"><span class="filepath"> /flashaccess/authn/v4/*</span> </li> 
     <li id="li-4DD6CBBE939F4E6EABA474E3DCCBD893"><span class="filepath"> /flashaccess/authn/v5/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">사용자 인증을 위한 URL. 이 URL은 Adobe 액세스 클라이언트 API를 사용하여 사용자 인증을 수행하는 경우에만 액세스할 수 있어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-yxs-rdn-44"> 
     <li id="li-49B9987ED6E14FADA66727448F923F84"><span class="filepath"> /flashaccess/license/v1/*</span> </li> 
     <li id="li-BF4A415E573C4C728E24D548F53D923C"><span class="filepath"> /flashaccess/license/v3/*</span> </li> 
     <li id="li-E6C551DDA030429B9D0073D2685B778A"><span class="filepath"> /flashaccess/license/v4/*</span> </li> 
     <li id="li-57811F4CD7304DBDAFADD65244AED0D9"><span class="filepath"> /flashaccess/license/v5/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">최종 사용자에게 라이선스를 발급하기 위한 URL. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-ibl-5dn-44"> 
     <li id="li-189BE370CD5044F988A42335C3BFE420"><span class="filepath"> /flashaccess/sync/v3</span> </li> 
     <li id="li-B333B85FFE8A46DD884595B0A620B4EE"><span class="filepath"> /flashaccess/sync/v4</span> </li> 
     <li id="li-E4771D3C5AA5454CA1EDCFAA3E027CC1"><span class="filepath"> /flashaccess/sync/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">동기화 요청에 대한 URL입니다. 이 URL은 라이센스에 동기화 요구 사항을 지정하는 경우에만 액세스할 수 있어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-plq-ydn-44"> 
     <li id="li-81C96F93BA904C8C95B907F1A77E6494"><span class="filepath"> /flashaccess/domain/v3</span> </li> 
     <li id="li-40F0952F09674CA3B9AAFB5A62F9D02E"><span class="filepath"> /flashaccess/domain/v4</span> </li> 
     <li id="li-3ADE44B959B548F8A31A6FF08537AF46"><span class="filepath"> /flashaccess/domain/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">도메인 등록용 URL. 이 URL은 도메인 지원을 구현하는 경우에만 액세스할 수 있어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-btm-c2n-44"> 
     <li id="li-3535EDF7C644406FAC471D4234C4AF98"><span class="filepath"> /flashaccess/dereg/v3</span> </li> 
     <li id="li-AB33657BC7E140E695767710DF7AEC72"><span class="filepath"> /flashaccess/dereg/v4</span> </li> 
     <li id="li-D15B32BCD4674269A3A2644DD5204707"><span class="filepath"> /flashaccess/dereg/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">도메인 등록 취소에 대한 URL. 이 URL은 도메인 지원을 구현하는 경우에만 액세스할 수 있어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/headerconversion/v1/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">클라이언트가 FMRMS 1.x DRM 메타데이터를 Adobe 액세스 DRM 메타데이터로 변환하기 위해 사용하는 URL. </p> <p class="- topic/p ">참고:<i class="+ topic/ph hi-d/i ">이 URL은 SSL(HTTPS)</i>을 사용해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /edcws/services/urn:EDCLicenseService/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">LiveCycle Rights Management ES 웹 서비스 URL. 이전 버전의 FMRMS를 사용하여 컨텐츠를 게시한 경우 이 URL을 통해 이전 클라이언트가 서버에 연결할 수 있으며 Adobe 액세스로 업그레이드하라는 메시지가 표시됩니다. </p> <p class="- topic/p ">참고:<i class="+ topic/ph hi-d/i ">이 URL은 SSL(HTTPS)</i>을 사용해야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/lreturn/v5</span> </td> 
   <td colname="2" class="- topic/entry "> <p>라이센스 반환에 대한 URL. 라이센스 반환 지원을 구현하는 경우에만 URL에 액세스할 수 있어야 합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>내부 방화벽은 역방향 프록시를 통해 Adobe 액세스 라이센스 서버에 연결되고 위에 나열된 URL에만 연결되도록 허용해야 합니다. 확장성을 높이기 위해 역방향 프록시와 Adobe 액세스 간의 연결은 HTTP를 통해 수행됩니다.

## 나가는 URL {#section-FFF9F7BB353149F4A27F8788E9934A48}

라이센스 서버는 Adobe에서 다음 CRL을 다운로드하려면 방화벽을 통해 액세스해야 합니다.

* h<span></span>ttps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl
* ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl
* ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl
* ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl