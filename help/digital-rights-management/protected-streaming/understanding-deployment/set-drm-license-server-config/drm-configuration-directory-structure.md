---
title: 디렉터리 구조 구성
description: 디렉터리 구조 구성
copied-description: true
exl-id: e24d3df0-f723-4dad-84d5-984f3350353a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '16'
ht-degree: 0%

---

# 디렉터리 구조 구성{#configuration-directory-structure}

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
