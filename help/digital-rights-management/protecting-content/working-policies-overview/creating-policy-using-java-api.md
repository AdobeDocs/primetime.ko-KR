---
title: Java API를 사용하여 DRM 정책 생성
description: Java API를 사용하여 DRM 정책 생성
copied-description: true
exl-id: fcae76c3-4e51-449d-b6d5-2138bf1c583e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Java API를 사용하여 DRM 정책 생성 {#creating-a-drm-policy-with-the-java-api}

Java API를 사용하여 DRM 정책을 생성하려면 다음을 수행합니다.

1. 개발 환경을 설정하여에 나열된 모든 JAR 파일을 프로젝트에 포함합니다. [개발 환경을 설정합니다.](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. 만들기 `com.adobe.flashaccess.sdk.policy.Policy` 개체를 지정하고 권한, 라이선스 캐싱 기간 및 DRM 정책 종료 날짜를 포함한 속성을 지정합니다.

   ```java
   // Create a new DRM policy object.  
   // False indicates the DRM policy does not use license chaining.  
   Policy policy = new Policy(false);  
   
   policy.setName("DemoPolicy");  
   
   // Specify that the DRM policy requires authentication to obtain a license.  
   policy.setLicenseServerInfo(new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
   // A DRM policy must have at least one Right, typically the play right  
   PlayRight play = new PlayRight();  
   
   // Users can only view content for 24 hours.  
   play.setPlaybackWindow(24L * 60 * 60);  
   
   // Add the play right to the DRM policy.  
   List<Right> rightsList = new ArrayList<Right>();  
   rightsList.add(play);  
   policy.setRights(rightsList);  
   
   // Licenses can be stored on the client for 7 days after downloading  
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

1. DRM 직렬화 `Policy` 개체를 만들고 파일이나 데이터베이스에 저장합니다.

   ```java
   // Serialize the DRM policy  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("Created DRM policy with ID: " + policy.getId());  
   
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy.pol");  
   out.write(policyBytes);  
   out.close(); 
   ```

다음을 참조하십시오 [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] 참조 구현 명령줄 도구 [!DNL samples] 이 샘플 코드의 전체 소스에 대한 디렉토리입니다.
