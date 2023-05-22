---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
exl-id: 67056085-beb5-4f54-8962-369bc32d7907
source-git-commit: 79cab347d0daa01549fbf8a9b37bf0a91c14648e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 명령줄 사용 {#command-line-usage}

도구를 실행하려면 다음 구문을 사용합니다.

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` 응용 프로그램에 있는 AIR 응용 프로그램의 signatures.xml 파일에 대한 경로를 지정합니다 [!DNL META-INF] 디렉터리

* `signingcert` AIR 애플리케이션 서명에 사용되는 인증서를 지정합니다.

>[!NOTE]
>
>iOS 애플리케이션에 대한 게시자 ID를 확인하려면 `-s` 옵션을 선택하고 iOS 애플리케이션 서명에 사용되는 인증서를 지정합니다. ***Adobe Primetime은 액세스 보호 콘텐츠를 재생할 수 있는 iOS 애플리케이션을 빌드하는 데 필요합니다.***.
