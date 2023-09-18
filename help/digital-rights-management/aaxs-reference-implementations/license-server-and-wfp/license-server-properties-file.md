---
title: 라이선스 서버 속성 파일
description: 라이선스 서버 속성 파일
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 라이선스 서버 속성 파일 {#license-server-properties-file}

사용 [!DNL flashaccess-refimpl.properties] 참조 구현의 라이선스 서버 구성 요소를 구성하는 파일입니다. 최소한 전송 자격 증명 및 라이선스 서버 자격 증명과 관련된 속성을 구성해야 합니다. 자격 증명 파일의 위치는 `config.resourcesDirectory` 속성. 이 파일에는 콘텐츠 패키징과 관련된 몇 가지 속성도 포함되어 있습니다. 이러한 속성은 Flash 미디어 Rights Management 서버 1.x 메타데이터 변환에만 사용됩니다. 이 속성 파일의 값을 수정하는 경우 변경 사항을 적용하려면 라이센스 서버를 다시 시작해야 합니다.

Adobe 액세스에서 iOS 클라이언트에 원격 키 전달을 위한 라이선스 생성을 지원하려면에 키 서버 인증서를 지정해야 합니다. [!DNL flashaccess-refimpl.properties].

Adobe 액세스에 다음 속성이 추가되었습니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">속성 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> Adobe이 발급한 키 서버의 라이선스 서버 인증서. 메타데이터가 키 서버가 필요함을 나타내는 경우 이 인증서는 iOS 장치의 라이선스를 생성하는 데 사용됩니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">HSM에 저장된 키 서버의 Adobe 발급 라이선스 서버 인증서 앨리어스. HSM이 활성화된 경우 대신 이 속성을 사용합니다. <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>
