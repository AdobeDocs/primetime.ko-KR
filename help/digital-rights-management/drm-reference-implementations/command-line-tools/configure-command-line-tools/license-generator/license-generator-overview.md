---
title: 개요
description: 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# DRM 라이센스 생성기 {#license-generator}

사용 [!DNL AdobeLicenseGenerator.jar] 클라이언트가 라이센스 요청을 서버에 보내지 않고도 라이센스를 생성할 수 있습니다. 그런 다음 콘텐츠에 사전 생성된 라이선스를 포함하거나 단순 HTTP 웹 서버와 같은 다른 메커니즘을 통해 클라이언트에 라이선스를 제공할 수 있습니다.

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

* `metadata` - Adobe Primetime DRM 메타데이터를 포함합니다.

  다음을 사용하여 보호된 콘텐츠에서 이 파일을 검색할 수 있습니다. `-d -m` media Packager의 옵션입니다.

**이전에 생성한 라이선스 표시:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - 라이센스 생성기로 생성된 Adobe Primetime DRM 라이센스가 포함됩니다.

**표 6: 옵션**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 이름과 위치를 지정합니다. </p> <p class="- topic/p ">이름이나 위치를 지정하지 않으면 DRM 라이센스 생성기가 <span class="filepath"> flashaccesstools.properties</span> 를 입력합니다. </p> <p>참고: 명령줄에서 지정한 옵션이 구성 파일에서 지정한 옵션보다 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 이미 생성된 라이센스에 대한 정보를 표시합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 리프 라이선스를 생성하고 출력을 지정된 파일에 저장합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m 메타데이터-파일 이름</span> </td> 
   <td colname="2" class="- topic/entry "> 라이선스를 생성해야 하는 콘텐츠 메타데이터를 지정합니다. 이 옵션은 라이센스를 생성하는 데 필요합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o</span> 이(가) 설정되지 않았습니다. 오류가 발생합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 메시지가 표시되지 않고 덮어쓸 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>메타데이터에 여러 DRM 정책이 포함된 경우 라이센스를 생성하는 데 사용할 수 있는 DRM 정책 수를 지정할 수 있습니다. </p> <p>DRM 정책 수를 지정하지 않으면 첫 번째 DRM 정책이 자동으로 적용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">지정된 수신자에 대한 라이선스를 생성합니다. 장치 또는 도메인 인증서를 사용하고 여러 개의 인증서를 지정할 수 있습니다 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>여러 수신자에 대한 라이선스를 만드는 옵션입니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 루트 라이센스를 생성하고 지정한 파일에 출력을 저장합니다. </td> 
  </tr> 
 </tbody> 
</table>

## 구성 파일 속성 {#configuration-file-properties}

라이센스 생성기를 실행하기 전에 구성 파일에서 라이센스 생성기 속성 값을 지정해야 합니다.

>[!NOTE]
>
>다음을 포함하는 속성 이름의 경우 *n*, *n* 는 1로 시작하고 속성의 각 인스턴스에 대해 증가하는 정수를 나타냅니다.

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
   <td colname="2" class="- topic/entry "> <p>현재 지원되는 최소 클라이언트 버전을 설정합니다. 이 속성을 설정하지 않으면 기본적으로 모든 버전이 자동으로 지원됩니다. </p> <p>이 값을 설정하여 이전 클라이언트가 지원하지 않는 라이선스 요구 사항에 응답하는 방식을 제어할 수 있습니다. 지정 <span class="codeph"> x</span> (Adobe Primetime DRM x.0용) <span class="codeph"> x</span> 주요 릴리스 번호를 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 키 서버 인증서: 키 서버에서 사용하는 Adobe 발급 라이선스 서버 인증서입니다. 이 인증서는 메타데이터/DRM 정책이 iOS 장치에 키 전달을 위해 키 서버가 필요함을 나타내는 경우에만 적용됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 라이센스 서명을 위한 라이센스 서버 인증서를 포함하는 PKCS12 파일입니다. 이 속성은 인증서 및 개인 키가 포함된 .pfx 파일을 참조해야 합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">로 지정한 파일을 보호하는 암호 <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> 옵션을 선택합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>도메인 바인딩 라이선스를 생성하는 경우, 하나 이상의 도메인 CA 인증서를 지정하여 라이선스 발급자가 신뢰할 수 있는 도메인 권한을 표시해야 합니다. </p> <p>라이선스 수신자가 지정된 도메인 CA 중 하나에서 발급되지 않은 도메인 인증서인 경우 라이선스를 생성할 수 없습니다. 이 속성은 <span class="filepath"> .cer</span> PEM 또는 DER 형식의 인증서가 포함된 파일입니다. <span class="codeph">n</span> 는 1부터 단조롭게 증가해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">메타데이터 및 DRM 정책의 CEK 암호를 해독하기 위한 추가 라이선스 서버 자격 증명을 포함하는 선택적 PKCS12 파일입니다. 콘텐츠가 이전에 로 지정된 자격 증명 이외의 라이센스 서버 인증서와 함께 패키지된 경우 추가 자격 증명을 구성할 수 있습니다 <span class="codeph"> licensegen.sign.certfile</span>. 이 속성은 다음을 참조해야 합니다. <span class="filepath"> .pfx</span> 인증서 및 개인 키가 포함된 파일입니다. <span class="codeph">n</span> 는 1부터 단조롭게 증가해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>암호는 로 지정한 파일을 보호하기 위해 적용됩니다.<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> 속성. </p> </td> 
  </tr> 
 </tbody> 
</table>
