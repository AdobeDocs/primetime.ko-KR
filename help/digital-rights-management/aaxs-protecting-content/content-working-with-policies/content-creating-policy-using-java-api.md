---
seo-title: Java API를 사용하여 정책 만들기
title: Java API를 사용하여 정책 만들기
uuid: c653548d-4abf-46b9-8669-d68b966da359
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Java API를 사용하여 정책 만들기 {#creating-a-policy-using-the-java-api}

Java API를 사용하여 정책을 만들려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 [설정에 언급된 모든 JAR 파일을](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 포함합니다.
1. 개체를 만들고 권한, 라이선스 캐싱 기간 및 정책 종료 날짜와 같은 속성을 지정합니다. `com.adobe.flashaccess.sdk.policy.Policy`

   ```java
     // Create a new Policy object.  
     // False indicates the policy does not use license chaining.  
     Policy policy = new Policy(false);  
   
     policy.setName("DemoPolicy");  
   
     // Specify that the policy requires authentication to obtain a license.  
     policy.setLicenseServerInfo  
      (new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
     // A policy must have at least one Right, typically the play right  
     PlayRight play = new PlayRight();  
   
     // Users may only view content for 24 hours.  
     play.setPlaybackWindow(24L * 60 * 60);  
   
     // Add the play right to the policy.  
     List<Right> rightsList = new ArrayList<Right>();  
     rightsList.add(play);  
     policy.setRights(rightsList);  
   
     // Licenses may be stored on the client for 7 days after downloading  
     policy.setLicenseCachingDuration(7L * 24 * 60 * 60);  
     try {  
      // Content will expire December 31, 2010  
      SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
      policy.setPolicyEndDate(dateFormat.parse("2010-12-31"));  
     } catch (ParseException e) {  
      // Invalid date specified in dateFormat.parse()  
      e.printStackTrace();  
     }
   ```

1. 개체를 `Policy` 직렬화하고 파일 또는 데이터베이스에 저장합니다.

   ```java
     // Serialize the policy  
     byte[] policyBytes = policy.getBytes();  
     System.out.println("Created policy with ID: " + policy.getId());  
   
     // Write the policy to a file.   
     // Alternatively, the policy may be stored in a database.  
     FileOutputStream out = new FileOutputStream("demopolicy.pol");  
     out.write(policyBytes);  
     out.close();
   ```

이 샘플 코드의 전체 소스는 *com.adobe.flashaccess.samples.policy.CreatePolicy를* [!DNL samples]참조하십시오.
