---
description: Protected Streaming용 Adobe Access Server에는 글로벌 구성 파일(flashaccess-global.xml)과 각 테넌트에 대한 테넌트 구성 파일(flashaccess-tenant.xml)의 두 가지 구성 파일이 필요합니다.
title: 디렉터리 구조 구성
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 라이선스 서버 구성 파일 및 구성 디렉터리 구조 {#configuration-directory-structure}

Adobe Access Server for Protected Streaming에는 전역 구성 파일(flashaccess-global.xml)과 각 테넌트에 대한 테넌트 구성 파일(flashaccess-tenant.xml)의 두 가지 구성 파일이 필요합니다.

Adobe 구성 파일을 편집한 후에는 보호된 스트리밍용 Adobe Access Server과 함께 제공되는 유틸리티를 사용하여 파일이 제대로 구성되어 있는지 확인하는 것이 좋습니다. 자세한 내용은 &quot;[구성 검사기](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

구성 파일에서 암호를 일반 텍스트로 사용할 수 없도록 하려면 전역 및 테넌트 구성 파일에 지정된 모든 암호를 암호화해야 합니다. 암호의 암호화와 관련된 자세한 내용은 &quot;[암호 스크램블러](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

구성 디렉토리의 구조는 다음과 같습니다.

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```
