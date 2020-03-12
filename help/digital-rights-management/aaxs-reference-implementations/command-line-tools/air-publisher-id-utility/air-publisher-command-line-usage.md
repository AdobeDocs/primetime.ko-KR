---
seo-title: 명령줄 사용
title: 명령줄 사용
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

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

* 
   * `signaturefile`* 응용 프로그램 [!DNL META-INF] 디렉토리에 있는 AIR 응용 프로그램의 signatures.xml 파일의 경로를 지정합니다.

* `signingcert` air 응용 프로그램을 서명하는 데 사용되는 인증서를 지정합니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>iOS 응용 프로그램의 게시자 ID를 확인하려면 `-s` 옵션을 사용하고 iOS 응용 프로그램 서명에 사용되는 인증서를 지정합니다. ***Adobe Primetime은 액세스 보호된 콘텐츠를***&#x200B;재생할 수 있는 iOS 애플리케이션을 구축하는 데 필요합니다.

