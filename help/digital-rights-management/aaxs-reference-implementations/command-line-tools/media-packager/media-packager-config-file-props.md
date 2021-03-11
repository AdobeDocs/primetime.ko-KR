---
title: 구성 파일 속성
description: 구성 파일 속성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# 구성 파일 속성 {#configuration-file-properties}

Media Packager를 실행하기 전에 Media Packager 속성 값을 지정합니다. 구성 파일은 다음 속성을 지정합니다. 속성 이름에 포함* n*이 있는 경우 *n*&#x200B;은 속성의 각 인스턴스에 대해 1로 시작하여 증가하는 정수를 나타냅니다.

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
   <td colname="2" class="- topic/entry "> 비디오 내용을 암호화할 것인지 여부를 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 오디오를 암호화할 것인지 여부를 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">FLV에서 스크립트 데이터를 암호화할 것인지 여부를 나타냅니다. <i class="+ topic/ph hi-d/i "></i> onMetaDataand  <i class="+ topic/ph hi-d/i "></i> onXMPscript 데이터 태그는 이 옵션이 활성화되어 있더라도 비밀번호화되지 않습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">비디오 암호화 수준을 나타냅니다. 높은 값은 모든 비디오 컨텐츠를 암호화하는 데 사용되며 중간 값과 낮음 값은 H.264 내용이 포함된 F4V 파일의 비디오 내용 부분을 암호화하는 데 사용됩니다. </p> <p class="- topic/p ">value = <span class="codeph"> 높음 | 중간 | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">값이 0보다 크면 파일 시작 부분에 지정된 컨텐츠 시간(초)이 암호화되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.unequivalid.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">키를 암호화하는 데 사용되는 라이센스 서버 인증서 파일입니다. <span class="codeph"> encrypt.keys.비대칭.certfile</span> 속성은 인증서만 포함하는 파일을 지정합니다(PEM 또는 DER 형식을 사용할 수 있음). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 속성은 컨텐츠에 적용할 정책 목록을 만드는 데 반복적으로 사용됩니다. <span class="codeph"> 값</span> 이 1 이상인 정수를 반환합니다. 클라이언트는 기본적으로 첫 번째 인스턴스를 사용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 서버 URL. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이센스 서버의 전송 인증서. 이 속성은 인증서 전용(PEM 또는 DER 형식을 사용할 수 있음)을 포함하는 <span class="filepath"> .cer</span> 파일을 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">콘텐츠 서명을 위한 패키지 자격 증명을 포함하는 PKCS12 파일입니다. <span class="codeph"> encrypt.sign.certfile</span>은 인증서 및 개인 키가 포함된 <span class="filepath"> .pfx</span> 파일을 참조해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><span class="codeph"> encrypt.sign.certfile</span>에서 지정한 파일을 보호하는 데 사용되는 암호입니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">패키징되는 컨텐츠에 대한 라이선스를 발행하는 데 필요한 최소 서버 버전을 설정합니다. x(Adobe Access x.0)를 지정합니다. 여기서 x = 주 릴리스 번호입니다. Adobe Access 3.0 이전의 서버는 이 설정을 지원하지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">정책 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span>에 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>에서 지정한 것과 다른 전송 인증서를 사용하는 서버에 도메인 등록이 필요한 경우 도메인 전송 인증서를 제공해야 합니다. </p> <p class="- topic/p ">이 속성은 인증서만 포함하는 파일을 지정합니다(PEM 또는 DER 형식을 사용할 수 있음). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이센스 키를 지정합니다. 키를 지정하지 않으면 키가 임의로 생성됩니다. 키 회전이 활성화되지 않으면 내용을 암호화하는 데 사용되는 키입니다. </p> <p class="- topic/p ">키 회전이 활성화되면 이 키를 사용하여 순환 키를 보호합니다. 키는 길이가 16바이트입니다. 16진수 값으로 지정됩니다. 16진수 값 사이의 공백은 선택 사항입니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">키 회전이 활성화되는지 여부를 지정합니다. false(기본값)로 설정하면 키 회전이 비활성화되고 마스터 CEK를 사용하여 컨텐츠의 모든 샘플을 암호화합니다. </p> <p class="- topic/p ">true로 설정하면 키 회전이 활성화되고 다른 키를 사용하여 내용의 일부를 암호화할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">키 회전이 활성화된 경우 컨텐츠를 암호화하는 데 사용되는 회전된 키의 시퀀스입니다. 키를 지정하지 않으면 키가 무작위로 생성됩니다. 키는 길이가 16바이트여야 하며 16진수 값으로 지정해야 합니다. </p> <p class="- topic/p ">16진수 값 사이의 공백은 선택 사항입니다. <i class="+ topic/ph hi-d/i ">1부터 단조롭게 </i> 증가해야 합니다. 여러 키를 지정하면 지정된 순서대로 키가 순환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">컨텐츠 샘플을 암호화하는 데 순환 키를 사용할 간격(초)을 지정합니다. </p> <p class="- topic/p ">내용의 이 시간이 암호화되면 다음 순환 키가 사용됩니다. 키 회전이 활성화되어 있고 간격을 지정하지 않으면 15분마다 키가 회전됩니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">true인 경우 라이선스를 받을 수 있는 라이센스 서버가 없습니다. 라이선스는 임베디드 또는 비밴드(out-of-band)로 가져와야 합니다. 지정하지 않으면 기본값이 false입니다. Adobe Access Professional에서만 지원됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

