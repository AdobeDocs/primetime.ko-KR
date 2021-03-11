---
title: 암호화된 콘텐츠 패키지
description: 암호화된 콘텐츠 패키지
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# 암호화된 내용 패키지{#package-encrypted-content}

1. `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 디렉토리를 로컬 파일 시스템에 복사합니다.
1. 로컬 `Command Line Tools\` 폴더에서 `flashaccesstools.properties` 파일을 업데이트하여 서버와 함께 사용할 수 있습니다.

   다음 속성 이상을 수정해야 합니다.

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`:라이센스 서버 인증서 경로(일반적으로  [!DNL .cer]또는  [!DNL .der] 로 끝남) [!DNL .pem].

   * `encrypt.license.serverurl=[license-server-url]`:라이센스 서버 URL(예:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`:전송 인증서의 경로(일반적으로  [!DNL .cer],  [!DNL .der]또는  [!DNL .pem]로 끝남).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`:Packager 인증서의 경로(다음으로  [!DNL .pfx]끝남).

   * `encrypt.sign.certpass=[password]`:Packager 인증서의 암호입니다.
   >[!NOTE]
   >
   >암호를 스크램블하지 않도록 하십시오.

1. 정책을 만듭니다.

   로컬 `Command Line Tools\` 폴더에서 다음 명령을 실행합니다.

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   이 명령은 익명 라이센스 서버 인증( `-x` 옵션)을 사용하는 [!DNL examplepolicy.pol]이라는 정책 파일을 만듭니다.
1. 로컬 `Command Line Tools\` 폴더에 암호화할 MP4, FLV 또는 F4V 비디오 파일을 복사합니다.
1. 콘텐츠를 패키징합니다.

   소스 비디오 파일이 [!DNL sample.mp4]이라고 가정합니다. 로컬 `Command Line Tools\` 폴더에서 다음 명령을 실행합니다.

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >HLS, HDS 또는 DASH 컨텐츠를 패키징하려면 [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)와 같은 다른 패키지 도구를 사용해야 합니다.

1. 암호화된 파일 객체(이 경우 [!DNL sample_encrypted.mp4] 및 [!DNL sample_encrypted.mp4.metadata])를 `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`에 복사합니다.

이 시점에서 프로세스의 패키징 단계를 완료했습니다.

>[!NOTE]
>
>내용 패키징, 정책 만들기 등을 위한 명령줄 도구에 대한 자세한 내용은 [Adobe Primetime DRM 명령줄 도구](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md)를 참조하십시오.
