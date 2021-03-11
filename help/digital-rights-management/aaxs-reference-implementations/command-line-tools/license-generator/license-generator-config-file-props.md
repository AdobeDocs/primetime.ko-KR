---
title: 구성 파일 속성
description: 구성 파일 속성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 구성 파일 속성 {#configuration-file-properties}

라이센스 생성기를 실행하기 전에 라이센스 생성기 속성 값을 지정합니다. 구성 파일은 다음 속성을 지정합니다. *n*&#x200B;이 포함된 속성 이름의 경우 *n*&#x200B;은 속성의 각 인스턴스에 대해 1로 시작하여 증가하는 정수를 나타냅니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 속성 </th> 
   <th colname="2" class="- topic/entry entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> 지원되는 최소 클라이언트 버전을 설정합니다. 설정하지 않은 경우 기본적으로 모든 버전이 지원됩니다. 이 값을 설정하여 이전 클라이언트가 지원하지 않는 라이센스 요구 사항에 응답하는 방식을 제어할 수 있습니다. x(Adobe Access x.0의 경우)를 지정합니다. 여기서 x는 주 릴리스 번호입니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 키 서버 인증서(키 서버에서 사용하는 Adobe 발급 라이선스 서버 인증서). 이 인증서는 메타데이터/정책이 키 서버가 iOS 장치에 배달되는 데 필요함을 나타내는 경우에만 사용됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licsegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 라이센스 서명을 위한 라이센스 서버 자격 증명을 포함하는 PKCS12 파일입니다. 이 속성은 인증서 및 개인 키가 포함된 .pfx 파일을 참조해야 합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licsegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile에서 지정한 파일을 보호하는 데 사용되는 암호입니다.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licsegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> 도메인 바인딩된 라이선스를 생성하는 경우 하나 이상의 도메인 CA 인증서를 지정하여 이 라이선스 발급자가 신뢰하는 도메인 권한을 표시해야 합니다. 라이선스 받는 사람이 지정된 도메인 CA 중 하나에서 발급되지 않은 도메인 인증서인 경우 라이선스를 생성할 수 없습니다. 이 속성은 인증서만 포함하는 .cer 파일을 지정합니다(PEM 또는 DER 형식을 사용할 수 있음). n은 1부터 단조롭게 증가해야 합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.비대칭적.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">메타데이터 및 정책에서 CEK를 해독하기 위한 추가 라이센스 서버 자격 증명을 포함하는 선택적 PKCS12 파일. 컨텐츠가 이전에 <span class="codeph"> licensegen.sign.certfile</span>에서 지정한 인증서 이외의 라이센스 서버 인증서로 패키지된 경우 추가 자격 증명을 구성할 수 있습니다. 이 속성은 인증서 및 개인 키가 포함된 <span class="filepath"> .pfx</span> 파일을 참조해야 합니다. n은 1부터 단조롭게 증가해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.비대칭.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">다음에 의해 지정된 파일을 보호하는 데 사용되는 암호: <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.비대칭적.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

