---
seo-title: 개요
title: 개요
uuid: 857390be-dd14-46c0-b8f7-2bc661c515d4
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# DRM 라이선스 생성기 {#license-generator}

클라이언트 [!DNL AdobeLicenseGenerator.jar] 가 라이선스 요청을 서버에 보내지 않고도 라이선스를 생성하는 데 사용합니다. 그런 다음 컨텐츠에 사전 생성된 라이센스를 포함하거나 간단한 HTTP 웹 서버와 같은 다른 메커니즘을 통해 라이센스를 클라이언트에 전달할 수 있습니다.

## 라이선스 생성기 명령줄 사용 {#license-generator-command-line-usage}

**라이선스 생성:**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata` - Adobe Primetime DRM 메타데이터 포함

   Media Packager의 옵션을 사용하여 보호된 내용에서 이 파일을 검색할 수 `-d -m` 있습니다.

**이전에 생성된 라이센스 표시:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - 라이센스 생성기에서 생성된 Adobe Primetime DRM 라이센스가 포함되어 있습니다.

**표 6:옵션**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 이름과 위치를 지정합니다. </p> <p class="- topic/p ">이름이나 위치를 지정하지 않으면 DRM License Generator가 현재 작업 디렉토리에서 flashaccesstools. <span class="filepath"> properties</span> 를 검색합니다. </p> <p>참고: 명령줄에서 지정하는 옵션은 구성 파일에서 지정한 옵션보다 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 이미 생성된 라이선스에 대한 정보를 표시합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 리프 라이센스를 생성하여 출력을 지정된 파일에 저장합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 라이선스를 생성해야 하는 컨텐츠 메타데이터를 지정합니다. 이 옵션은 라이센스를 생성하는 데 필요합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">대상 파일을 덮어써야 하는지 묻지 않습니다. 대상 파일이 이미 있고 -o <span class="codeph"> 를</span> 설정하지 않은 경우 오류가 발생합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 메시지가 표시되지 않고 덮어쓸 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>메타데이터에 여러 DRM 정책이 포함된 경우 라이선스를 생성하는 데 사용할 수 있는 DRM 정책 수를 지정할 수 있습니다. </p> <p>DRM 정책 수를 지정하지 않으면 첫 번째 DRM 정책이 자동으로 적용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">지정된 수신자에 대한 라이센스를 생성합니다. 장치 또는 도메인 인증서를 사용할 수 있으며 여러 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>옵션을 지정하여 여러 수신자를 위한 라이센스를 만들 수 있습니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 루트 라이센스를 생성하고 지정된 파일에 출력을 저장합니다. </td> 
  </tr> 
 </tbody> 
</table>

## 구성 파일 속성 {#configuration-file-properties}

License Generator를 실행하기 전에 구성 파일에서 License Generator 속성의 값을 지정해야 합니다.

>[!NOTE]
>
>n이 포함된 속성 이름 *의*&#x200B;경우 *n* 은 속성의 각 인스턴스에 대해 1로 시작하고 증가되는 정수를 나타냅니다.

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
   <td colname="2" class="- topic/entry "> <p>현재 지원되는 최소 클라이언트 버전을 설정합니다. 이 속성을 설정하지 않으면 기본적으로 모든 버전이 자동으로 지원됩니다. </p> <p>이 값을 설정하여 이전 클라이언트가 지원하지 않는 라이센스 요구 사항에 응답하는 방식을 제어할 수 있습니다. 주요 릴리스 번호를 나타내는 <span class="codeph"> x</span> (Adobe Primetime DRM x.0) <span class="codeph"> 를</span> 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 키 서버 인증서 - 키 서버에서 사용하는 Adobe에서 발급한 라이센스 서버 인증서입니다. 이 인증서는 메타데이터/DRM 정책이 키 서버가 iOS 장치에 배달되어야 한다고 표시하는 경우에만 적용됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licsegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 라이센스 서명을 위한 라이센스 서버 자격 증명을 포함하는 PKCS12 파일. 이 속성은 인증서 및 개인 키가 포함된 .pfx 파일을 참조해야 합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licsegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">licensegen.sign.certfile 옵션으로 지정한 파일을 <span class="+ topic/ph pr-d/codeph codeph"> 보호하는 암호입니다</span> . </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licsegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>도메인 바인딩된 라이선스를 생성하는 경우 라이선스 발급자가 신뢰할 수 있는 도메인 기관을 나타내는 하나 이상의 도메인 CA 인증서를 지정해야 합니다. </p> <p>라이선스 수신자가 지정된 도메인 CA 중 하나에서 발급되지 않은 도메인 인증서인 경우 라이선스를 생성할 수 없습니다. 이 속성은 PEM 또는 DER 형식의 인증서를 포함하는 <span class="filepath"> .cer</span> 파일을 지정합니다. <span class="codeph">1부터</span> 시작하여 단조로움을 증가시켜야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">메타데이터 및 DRM 정책에서 CEK를 해독하기 위한 추가 라이센스 서버 자격 증명을 포함하는 선택적 PKCS12 파일. 이전에 content가 licensegen.sign.certfile을 통해 지정된 자격 증명이 아닌 라이센스 서버 인증서로 패키지화된 경우 추가 자격 증명을 구성할 수 <span class="codeph"> 있습니다</span>. 이 속성은 인증서 및 개인 키가 포함된 <span class="filepath"> .pfx</span> 파일을 참조해야 합니다. <span class="codeph">1부터</span> 시작하여 단조로움을 증가시켜야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>이 비밀번호는 licensegen.keys.비대칭적.licenseServerCredential.n<span class="+ topic/ph pr-d/codeph codeph"></span> 속성으로 지정한 파일을 보호하기 위해 적용됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>