---
title: Java API를 사용하여 정책 업데이트
description: Java API를 사용하여 정책 업데이트
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Java API를 사용하여 정책 업데이트 {#updating-a-policy-using-the-java-api}

Java API를 사용하여 정책을 업데이트하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고에 언급된 모든 JAR 파일을 포함하십시오. [개발 환경 설정](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 을 참조하십시오.
1. 만들기 `Policy` 를 클릭하고 파일 또는 데이터베이스에서 정책을 읽습니다.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 업데이트 `Policy` 이름 및 사용 규칙과 같은 속성을 설정하여 객체를 만듭니다.

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

1. 업데이트된 항목 직렬화 `Policy` 개체를 만들고 파일이나 데이터베이스에 저장합니다.

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

이 샘플 코드의 전체 소스는 다음을 참조하십시오. `com.adobe.flashaccess.samples.policy.UpdatePolicy` 참조 구현 명령줄 도구 &quot;samples&quot; 디렉터리에서
