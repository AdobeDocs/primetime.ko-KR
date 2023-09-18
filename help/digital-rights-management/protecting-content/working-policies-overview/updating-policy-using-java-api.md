---
title: Java API를 사용하여 DRM 정책 업데이트
description: Java API를 사용하여 DRM 정책 업데이트
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Java API를 사용하여 DRM 정책 업데이트 {#updating-a-drm-policy-with-the-java-api}

Java API를 사용하여 DRM 정책을 업데이트하려면 다음을 수행하십시오.

1. 개발 환경을 설정하여에 나열된 모든 JAR 파일을 프로젝트에 포함합니다. [개발 환경 설정](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. DRM 생성 `Policy` 를 클릭하고 파일이나 데이터베이스에서 DRM 정책을 읽습니다.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. DRM 업데이트 `Policy` 이름 및 사용 규칙과 같은 속성을 설정하여 객체를 만듭니다.

   ```java
   // Change the DRM policy name.  
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

1. 업데이트된 DRM 직렬화 `Policy` 개체를 만들고 파일이나 데이터베이스에 저장합니다.

   ```java
   // Serialize the DRM policy.  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("New DRM policy revision number: "  
       +  policy.getRevision());      
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
   out.write(policyBytes);  
   out.close();
   ```

다음을 참조하십시오 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 참조 구현 명령줄 도구 [!DNL samples] 이 샘플 코드의 소스에 대한 디렉토리입니다.
