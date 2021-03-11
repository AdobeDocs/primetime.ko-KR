---
title: 라이센스 서버 속성 파일
description: 라이센스 서버 속성 파일
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 라이센스 서버 속성 파일 {#license-server-properties-file}

[!DNL flashaccess-refimpl.properties] 파일을 사용하여 참조 구현의 라이센스 서버 구성 요소를 구성합니다. 전송 자격 증명 및 라이센스 서버 자격 증명과 관련된 속성은 최소한 구성해야 합니다. 자격 증명 파일의 위치는 `config.resourcesDirectory` 속성에 의해 지정된 디렉토리에 상대적인 것으로 지정해야 합니다. 이 파일에는 컨텐츠 패키징과 관련된 여러 속성이 포함되어 있습니다.이러한 속성은 Flash Media Rights Management Server 1.x 메타데이터 변환에만 사용됩니다. 이 속성 파일의 값을 수정하는 경우 변경 사항을 적용하려면 라이센스 서버를 다시 시작해야 합니다.

Adobe 액세스의 iOS 클라이언트에 원격 키 전달에 대한 라이선스 생성을 지원하려면 키 서버 인증서를 [!DNL flashaccess-refimpl.properties]에 지정해야 합니다.

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
   <td colname="2" class="- topic/entry "> Adobe에서 발행한 키 서버의 라이센스 서버 인증서 이 인증서는 메타데이터에 키 서버가 필수임을 나타내는 경우 iOS 장치에 대한 라이센스를 생성하는 데 사용됩니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">HSM에 저장된 키 서버의 Adobe 발급 라이선스 서버 인증서의 별칭입니다. HSM이 활성화되면 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> 대신 이 속성을 사용합니다. </td> 
  </tr> 
 </tbody> 
</table>

