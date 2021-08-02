---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

* `signaturefile` 응용 프로그램 디렉토리에 있는 AIR 응용 프로그램의 signatures.xml 파일의 경로를  [!DNL META-INF] 지정합니다.

* `signingcert` AIR 응용 프로그램을 서명하는 데 사용되는 인증서를 지정합니다.

>[!NOTE]
>
>iOS 응용 프로그램의 게시자 ID를 결정하려면 `-s` 옵션을 사용하여 iOS 응용 프로그램을 서명하는 데 사용되는 인증서를 지정합니다. ***Adobe Primetime은 액세스 보호된 내용을 재생할 수 있는 iOS 애플리케이션을 구축하려면 필요합니다***.

