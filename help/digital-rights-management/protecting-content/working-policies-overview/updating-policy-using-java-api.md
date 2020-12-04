---
seo-title: Java API로 DRM 정책 업데이트
title: Java API로 DRM 정책 업데이트
uuid: ec21351c-900e-48f5-845a-c0b430c210d7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Java API {#updating-a-drm-policy-with-the-java-api}로 DRM 정책 업데이트

Java API로 DRM 정책을 업데이트하려면:

1. 개발 환경을 설정하고 프로젝트에 [개발 환경 설정](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)에 나열된 모든 JAR 파일을 포함합니다.
1. DRM `Policy` 인스턴스를 만들고 파일 또는 데이터베이스에서 DRM 정책을 읽습니다.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 이름 및 사용 규칙과 같은 속성을 설정하여 DRM `Policy` 개체를 업데이트합니다.

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

1. 업데이트된 DRM `Policy` 개체를 직렬화하고 파일 또는 데이터베이스에 저장합니다.

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

이 샘플 코드의 소스는 참조 구현 명령줄 도구 [!DNL samples] 디렉토리의 `com.adobe.flashaccess.samples.policy.UpdatePolicy`을 참조하십시오.
