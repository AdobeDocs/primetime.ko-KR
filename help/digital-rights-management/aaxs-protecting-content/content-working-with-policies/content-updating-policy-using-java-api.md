---
title: Java API를 사용하여 정책 업데이트
description: Java API를 사용하여 정책 업데이트
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Java API {#updating-a-policy-using-the-java-api}을 사용하여 정책 업데이트

Java API를 사용하여 정책을 업데이트하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내에 [개발 환경 설정](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)에 언급된 모든 JAR 파일을 포함합니다.
1. `Policy` 인스턴스를 만들고 파일이나 데이터베이스에서 정책을 읽습니다.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 이름 및 사용 규칙과 같은 속성을 설정하여 `Policy` 개체를 업데이트합니다.

   ```java
     // Change the policy name.  
     policy.setName("UpdatedDemoPolicy");  
   
     // Add DRM module restrictions to the play right  
     for (Right r: policy.getRights()) {  
      if (r instanceof PlayRight) {  
       PlayRight pr = (PlayRight) r;  
       // Disallow Linux versions up to and including 1.9.  Allow  
       // all other OSes and Linux versions above 1.9  
       VersionInfo toExclude = new VersionInfo();  
       toExclude.setOS("Linux");  
       toExclude.setReleaseVersion("1.9");  
       Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
       exclusions.add(toExclude);  
       ModuleRequirements drmRestrictions = new ModuleRequirements();  
       drmRestrictions.setExcludedVersions(exclusions);  
       pr.setDRMModuleRequirements(drmRestrictions);  
       break;  
      }  
     }
   ```

1. 업데이트된 `Policy` 개체를 직렬화하고 파일 또는 데이터베이스에 저장합니다.

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

이 샘플 코드의 전체 소스는 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리의 `com.adobe.flashaccess.samples.policy.UpdatePolicy`을 참조하십시오.
