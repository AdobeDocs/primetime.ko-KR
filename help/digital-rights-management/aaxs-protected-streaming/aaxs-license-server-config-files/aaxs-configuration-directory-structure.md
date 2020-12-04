---
description: 보호된 스트리밍을 위한 Adobe Access Server을 사용하려면 글로벌 구성 파일(flashaccess-global.xml)과 각 테넌트에 대한 테넌트 구성 파일(flashaccess-tenant.xml)의 두 가지 유형의 구성 파일이 필요합니다.
seo-description: 보호된 스트리밍을 위한 Adobe Access Server을 사용하려면 글로벌 구성 파일(flashaccess-global.xml)과 각 테넌트에 대한 테넌트 구성 파일(flashaccess-tenant.xml)의 두 가지 유형의 구성 파일이 필요합니다.
seo-title: 구성 디렉토리 구조
title: 구성 디렉토리 구조
uuid: c6cfc734-6b7c-4502-9bdb-c7aaca156e0e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 라이센스 서버 구성 파일 및 구성 디렉터리 구조 {#configuration-directory-structure}

보호 스트리밍을 위한 Adobe Access Server의 구성 파일 유형은 다음과 같습니다.전역 구성 파일(flashaccess-global.xml)과 각 테넌트에 대한 테넌트 구성 파일(flashaccess-tenant.xml)입니다.

구성 파일을 편집한 후 보호 스트리밍을 위해 Adobe Access Server과 함께 제공된 유틸리티를 사용하여 파일이 제대로 구성되어 있는지 확인하는 것이 좋습니다. 자세한 내용은 &quot;[구성 유효성 검사기](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;을 참조하십시오.

구성 파일의 투명 텍스트로 암호를 사용하지 않으려면 전역 및 테넌트 구성 파일에 지정된 모든 암호를 암호화해야 합니다. 암호 암호화에 대한 자세한 내용은 &quot;[암호 스크램블러](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;를 참조하십시오.

구성 디렉토리는 다음과 같은 구조를 가집니다.

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

