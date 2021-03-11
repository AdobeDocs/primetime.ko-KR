---
title: 서버 속성 참조
description: 서버 속성 참조
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---


# 서버 속성 참조{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## 개인화 서버

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> 구성 </th> 
   <th class="entry"> 설명 </th> 
   <th class="entry"> 예 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 전송 자격 증명 </td> 
   <td>전송 자격 증명은 클라이언트에서 받은 요청을 해독하고 다시 보낸 응답에 서명하는 데 사용됩니다. <span class="filepath"> AdobeInitial.properties</span> 파일을 전송 자격 증명 파일의 경로 및 암호화된 PKCS12 암호와 함께 적절하게 구성해야 합니다. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file =  </span> [PKCS12 파일(개인화 전송 인증서 및 키 포함)] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password=</span> [PKCS12 파일의 암호화된 암호] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 개인화 CA 자격 증명 </td> 
   <td>개인화 서버는 CA 자격 증명을 사용하여 발행되는 컴퓨터 인증서에 서명합니다. I15N CA 자격 증명 파일의 경로 및 암호화된 PKCS12 암호의 두 경로와 함께 <span class="filepath"> AdobeInitial.properties</span> 파일을 적절하게 구성해야 합니다. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file=</span> [PKCS12 파일(식별 CA 인증서 및 키 포함)] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password=</span> [PKCS12 파일의 암호화된 암호] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 개인화 암호화 자격 증명 </td> 
   <td> 개인화 서버는 암호화 자격 증명을 사용하여 개인화 서버로 전송해야 하는 중요한 파일을 암호화합니다. 예를 들어 이 인증서는 라이선스 마이그레이션을 지원하며 개인 설정 서버의 DRM 개인 키를 암호화하는 데에도 사용됩니다. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 콘텐트 캐시 </td> 
   <td>이러한 설정은 Indification Server가 콘텐트를 다운로드하는 위치와 콘텐트를 디스크에 캐시하는 위치를 제어합니다. 개인화 서버는 시작 시 컨텐츠 서버에 새 컨텐츠가 있는지 확인하고 이러한 속성에 지정된 빈도/시간에 대해 확인합니다. <p>온-프레미스 개인화 서버의 경우, 콘텐츠 캐시 데이터의 초기 세트를 포함했습니다. 캐시 폴더 자체가 아닌 캐시 폴더의 <i>CONTENTS</i>를 구성된 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> 위치에 복사해야 합니다. </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory=</span> [로컬 내용을 저장할 디렉토리(일반적으로 tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server=</span> [ECI 정보를 문의할 웹 서버(이 릴리스에서 <i>지원되지 않음</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout = </span> [연결 시간 초과, 초 단위] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency = </span> [서버를 폴링하는 빈도(일 단위)(최소 1일)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime=</span> [서버를 폴링할 시간(자정 이후 분 단위)] </li> 
    </ul> <p>캐시를 최신 상태로 유지하는 방법에 대한 <i>CRL 및 ECI 파일</i> 섹션을 읽으십시오. </p> </td> 
  </tr> 
  <tr> 
   <td> 개인화 CA CRL </td> 
   <td> <p>이 CRL(Certificate Revocation List) 배포 지점은 Indification Server에서 발행한 각 컴퓨터 인증서에 포함됩니다. 라이센스 서버의 컴퓨터 인증서 유효성 검사 동안 CRL은 인증서에 나열된 배포 지점(또는 이미 다운로드한 경우 캐시에서 읽기)에서 다운로드되고 인증서가 해지되지 않았는지 확인합니다. 개별 CA CRL을 생성 및 배포하는 프로세스를 진행한 후 이 서버 구성 변경을 수행하는 것이 좋습니다. 구성을 변경한 후 개인 정보 서버를 다시 시작합니다. </p> <p>CRL 배포 지점에 대한 URL을 설정하려면 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> 필드를 설정해야 합니다. </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldap=</span> [CRL 배포 지점] </li> 
    </ul> <p>예: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>라이센스 요청이 처리되면 라이센스 서버는 이 CRL을 자동으로 다운로드해야 합니다. </p> <p importance="high">참고:이 배포 지점은 Primetime DRM에서 유효성 확인을 하지 않은 <i>입니다. </i> 이 URL이 유효한지 확인해야 합니다. 잘못된 URL로 인한 오류는 라이센스 서버에서 유효성 검사 오류가 표시될 때까지 나타나지 않습니다. </p> </td> 
  </tr> 
  <tr> 
   <td> 로깅 </td> 
   <td>필요에 따라 로깅을 위해 <span class="filepath"> AdobeInitial.properties</span>를 구성합니다. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc=</span> [로그 파일을 만들 디렉토리] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [로그에 나타날 수 있는 가장 낮은 로그 메시지  <span class="codeph"> [DEBUG] | 정보]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName = </span> [로그 파일의 접두어. 날짜/시간 및 ".log" 확장명이 파일 이름에 추가됩니다. </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval = </span> [로그가 롤링 되는 빈도를 지정합니다.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize = </span> [이 크기에 도달하면 로그를 롤링(RollIntervalor RollSize에 도달하면 로그 <span class="codeph"> </span> 가  <span class="codeph"> </span> 롤링)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled=</span>[ [true] | false ] 개별 보고서를 생성하기 위해 Adobe에서 사용하는 데이터를 포함하는 별도의 파일을 생성할지 여부를 지정합니다.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName=</span> [보고서 로그 파일의 접두어. 날짜/시간 및 <span class="filepath"> .log</span> 확장명이 파일 이름에 추가됩니다. l<span class="codeph"> og.Level</span> 속성은 이 로그 파일에 적용되지 않지만 <span class="codeph"> log.RollInterval</span> 및 <span class="codeph"> log.RollSize</span> do.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 기타 </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key=</span> [컴퓨터 토큰에 포함되기 전에 HMAC 장치 정보에 사용된 암호화된 Base64 인코딩 키. 키는 개발/스테이징/프로덕션 환경에 대해 다를 수 있지만 특정 환경의 모든 서버에 대해서는 동일해야 합니다.] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server=</span> [키 세대 서버의 위치(키 서버 풀을 나타내는 단일 호스트/포트)] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize=</span> [대기열에 많은 키가 남아 있을 때 KGS에서 다른 키 일괄 가져오기] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout=</span> [상태 페이지에서 KGS를 ping하여 서버에 도달할 수 있는지 확인합니다. 지정된 시간 내에 응답을 받지 못하면 시간 초과됩니다.] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 키 생성 서버 {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> 구성 </th> 
   <th class="entry"> 설명 </th> 
   <th class="entry"> 예 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 키 생성 </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [키를 생성하는 데 사용할 스레드 수(컴퓨터에서 사용할 수 있는 프로세서 수와 동일해야 함)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize=</span> [일괄 처리당 생성할 키 수] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory = </span> [키 일괄 처리 파일을 저장할 디렉토리] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize = </span> [생성할 최대 키 일괄 처리 파일 수] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 로깅 </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc=</span> [로그 파일을 만들 디렉토리] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName = </span> [로그 파일의 접두어. 날짜/시간 및 <span class="filepath"> .log</span> 확장명이 파일 이름에 추가됩니다. </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [로그에 나타날 수 있는 가장 낮은 로그 메시지 수준] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval = </span> [로그가 롤링 되는 빈도를 지정합니다.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize = </span> [이 크기에 도달하면 로그를 롤링(RollIntervalor RollSize에 도달하면 로그 <span class="codeph"> </span> 가  <span class="codeph"> </span> 롤링)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
