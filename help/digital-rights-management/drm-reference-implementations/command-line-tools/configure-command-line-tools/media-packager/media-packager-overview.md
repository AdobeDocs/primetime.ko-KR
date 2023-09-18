---
title: 개요
description: 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# DRM 미디어 패키지 {#media-packager}

Media Packager 사용( [!DNL AdobePackager.jar])을 클릭하여 콘텐츠에 적용할 DRM 정책을 지정하고 암호화할 콘텐츠의 부분을 지정합니다. 예를 들어, 패키저가 비디오 데이터는 암호화하지만 오디오 데이터는 암호화하지 않도록 지정할 수 있습니다.

실행하기 전에 [!DNL AdobePackager.jar], 구성 파일의 Media Packager 속성 섹션에서 속성을 설정해야 합니다.

>[!NOTE]
>
>명령줄에서 모든 Media Packager 속성을 지정할 수도 있습니다.

## Media Packager 명령줄 사용 {#media-packager-command-line-usage}

**하나의 파일 패키지:**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` - 암호화할 파일의 이름입니다.
* `dest` - 암호화된 파일의 이름입니다.

  디렉토리를 지정하면 암호화된 파일이 소스 파일로 지정한 것과 동일한 파일 이름으로 지정된 디렉토리에 자동으로 저장됩니다. 그러나 소스 파일이 포함된 대상 디렉토리는 지정할 수 없습니다.

**동일한 키로 여러 파일 패키징** 다중 비트 전송률 지원의 경우:

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` - 암호화할 파일에 대한 일련의 공백으로 구분된 소스 항목입니다.
* `dest-directory` - 암호화된 콘텐츠를 작성할 대상 디렉터리입니다. 암호화된 파일은 소스 파일과 동일한 파일 이름을 사용하여 이 디렉토리에 자동으로 저장됩니다. 그러나 대상 디렉토리에는 소스 파일이 포함될 수 없습니다.

**암호화된 파일에 대한 정보 보기:**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**메타데이터 파일에 대한 정보 보기:**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 다음 값: [!DNL .metadata] drm 메타데이터가 포함된 파일.

>[!NOTE]
>
>패키지하는 동안 미디어 포장기는 더 이상 [!DNL .header] 기본적으로 파일입니다. 을(를) 생성하려면 [!DNL .header] 파일, 사용 `-h` 포장 중 옵션입니다.

**표 3: 옵션**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 이름과 위치를 지정합니다. </p> <p class="- topic/p ">이름이나 위치를 지정하지 않으면 DRM Media Packager가 <span class="filepath"> flashaccesstools.properties </span> 를 입력합니다. </p> <p>참고: 명령줄에서 지정한 옵션이 구성 파일에서 지정한 옵션보다 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> 암호화 파일 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이미 패키지된 파일에 대한 정보를 볼 수 있습니다. </p> <p class="- topic/p ">소스 및 대상 파일이 필요하지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> 메타데이터 파일 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">기존 메타데이터에 대한 정보를 볼 수 있습니다. </p> <p class="- topic/p ">소스 및 대상 파일이 필요하지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 옵션을 와 함께 적용할 때 패키지된 파일에서 DRM 정책을 추출합니다. <span class="codeph"> -d </span> 옵션을 선택합니다. </p> <p class="- topic/p ">파일은 파일 이름과 DRM 정책 식별자를 사용하여 암호화된 파일이 있는 동일한 디렉토리에 자동으로 생성됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 옵션을 와 함께 적용하면 패키지된 파일에서 DRM 헤더를 추출합니다. <span class="codeph"> -d </span> 옵션을 선택합니다. </p> <p class="- topic/p ">파일 이름 및 확장자를 사용하여 암호화된 파일이 있는 동일한 디렉터리에 파일이 자동으로 만들어집니다 <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 콘텐츠 세그먼트에 대한 고유 식별자를 지정합니다. </p> <p class="- topic/p ">식별자를 지정하지 않으면 대상 파일 이름이 자동으로 적용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> 값 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">콘텐츠 메타데이터에 추가할 사용자 지정 키/값을 지정합니다. </p> <p class="- topic/p ">여러 을 지정할 수 있습니다 <span class="codeph"> -k </span> 옵션. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 옵션을 와 함께 적용할 때 패키지된 파일에서 메타데이터 추출 <span class="codeph"> -d </span> 옵션을 선택합니다. </p> <p class="- topic/p ">파일은 파일 이름과 <span class="codeph"> .metadata </span> 확장명. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. </p> <p class="- topic/p ">대상 파일이 이미 있고 <span class="codeph"> -o </span> 가 설정되지 않은 경우 오류가 발생합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 존재하지 않는 한 메시지 표시 없이 대상 파일을 덮어씁니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 파일 이름 [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 정책을 포함하는 파일의 이름을 지정합니다. </p> <p class="- topic/p ">DRM 정책이 등록 정보 파일에 지정한 전송 인증서 이외의 전송 인증서를 사용하는 서버에 도메인 등록을 필요로 하는 경우 도메인 전송 인증서를 제공해야 합니다. </p> <p class="- topic/p ">여러 을 지정할 수 있습니다 <span class="codeph"> -p </span> 옵션. 클라이언트는 기본적으로 항상 첫 번째 옵션을 적용합니다. 명령줄에 지정한 값이 구성 파일에 지정한 값보다 우선합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 구성 속성 {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>* n*을 포함하는 속성 이름의 경우, *n* 는 1로 시작하고 속성의 각 인스턴스에 대해 증가하는 정수를 나타냅니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">속성 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> 비디오 콘텐츠를 암호화할지 여부를 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 오디오를 암호화할지 여부를 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>mp4s에서 스크립트 데이터를 암호화할지 여부를 나타냅니다. </p> <p><i class="+ topic/ph hi-d/i ">메타데이터</i> 및 <i class="+ topic/ph hi-d/i ">onXMP</i> 이 옵션을 활성화해도 스크립트 데이터 태그는 암호화되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">비디오 암호화 수준을 나타냅니다. </p> <p class="- topic/p ">값 <span class="codeph"> 높음</span> 은 모든 비디오 콘텐츠를 암호화하는 데 사용되지만, 의 값은 <span class="codeph"> 중간</span> 및 <span class="codeph"> 낮음</span> 는 H.264 콘텐츠를 포함하는 mp4 파일용 비디오 콘텐츠의 일부를 암호화하는 데 사용됩니다. </p> <p class="- topic/p ">값 = <span class="codeph"> 높음 | 중간 | 낮음</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.seconds암호화되지 않음</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">값이 0보다 크면 파일 시작 시 지정된 시간(초)의 콘텐츠가 암호화되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">키를 암호화하는 데 사용되는 라이선스 서버 인증서 파일입니다. </p> <p class="- topic/p ">다음 <span class="codeph"> encrypt.keys.asymmetric.certfile</span> 속성은 인증서만 포함하는 파일을 지정합니다(PEM 또는 DER 형식 허용 가능). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 속성은 콘텐츠에 적용할 DRM 정책 목록을 만드는 데 반복적으로 사용됩니다. <span class="codeph"> n</span> 값이 1 이상인 정수를 나타냅니다. 클라이언트는 기본적으로 첫 번째 인스턴스를 사용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 서버 URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 서버에 대한 전송 인증서입니다. </p> <p class="- topic/p ">이 속성은 <span class="filepath"> .cer</span> 인증서만 포함하는 파일(PEM 또는 DER 형식 허용 가능). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">콘텐츠 서명을 위한 패키지 자격 증명이 포함된 PKCS12 파일. </p> <p class="- topic/p ">다음 <span class="codeph"> encrypt.sign.certfile</span> 을(를) 참조해야 합니다. <span class="filepath"> .pfx</span> 인증서 및 개인 키가 포함된 파일입니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">에 지정된 파일을 보호하기 위해 적용할 수 있는 암호 <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">패키지되는 콘텐츠에 대한 라이선스를 발급하는 데 필요한 최소 서버 버전을 설정합니다. </p> <p class="- topic/p ">Primetime DRM x.0의 경우 x를 지정합니다. 여기서 x는 주요 릴리스 번호를 나타냅니다. Adobe Primetime 버전 3.0 이전의 모든 서버 버전은 이 설정을 지원하지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 정책인 경우 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 은(는) 사용자가 지정한 전송 인증서 이외의 전송 인증서를 지원하는 서버에 도메인 등록을 필요로 합니다. <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>그런 다음 도메인 전송 인증서 요구 사항을 제공해야 합니다. </p> <p class="- topic/p ">이 속성은 인증서만 포함하는 파일을 지정합니다(PEM 또는 DER 형식 허용 가능). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 키를 지정합니다. </p> <p class="- topic/p ">키를 지정하지 않으면 키가 임의로 생성됩니다. 키 회전을 활성화하지 않은 경우 이 키를 사용하여 콘텐츠를 암호화할 수 있습니다. </p> <p class="- topic/p ">키 회전을 활성화하면 이 키를 사용하여 회전 키를 보호할 수 있습니다. 키는 16바이트 길이여야 하며 16진수 값으로 지정해야 합니다. 16진수 값 사이의 공백은 선택 사항입니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">키 순환을 사용할지 여부를 지정합니다. </p> <p class="- topic/p ">기본 설정인 false로 설정하면 키 회전이 비활성화되고 마스터 CEK가 사용되어 콘텐츠의 모든 샘플을 암호화합니다. </p> <p class="- topic/p ">true로 설정하면 키 회전이 활성화되고 다른 키를 사용하여 콘텐츠의 세그먼트를 암호화할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">키 회전이 활성화된 경우 콘텐츠를 암호화하도록 지정할 수 있는 회전된 키 시퀀스. </p> <p class="- topic/p ">키를 지정하지 않으면 키가 임의로 생성됩니다. 키는 16바이트 길이여야 하며 16진수 값으로 지정해야 합니다. </p> <p class="- topic/p ">16진수 값 사이의 공백은 선택 사항입니다. <i class="+ topic/ph hi-d/i ">n</i> 은(는) 1부터 시작하여 단조롭게 증가해야 합니다. 키를 여러 개 지정하면 지정한 순서대로 키가 순환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">콘텐츠 샘플을 암호화하기 위해 회전 키를 적용할 수 있는 시간 간격을 초 단위로 지정합니다. </p> <p class="- topic/p ">콘텐츠가 암호화된 시간 간격이 경과하면 다음 회전 키가 적용됩니다. 키 회전을 활성화했지만 시간 간격을 지정하지 않은 경우 키는 15분마다 자동으로 회전됩니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 옵션이 true로 설정되면 라이센스를 얻을 수 있는 라이센스 서버를 사용할 수 없습니다. </p> <p class="- topic/p ">라이센스는 임베드되거나 대역 외로 획득되어야 합니다. 다른 값을 지정하지 않는 한 기본값은 false로 설정됩니다. 이 옵션은 Primetime DRM Professional에서만 지원됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
