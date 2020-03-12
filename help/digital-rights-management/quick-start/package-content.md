---
seo-title: 암호화된 컨텐츠 패키지
title: 암호화된 컨텐츠 패키지
uuid: 1e271167-107d-41df-8a7c-3075cb3acc0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 암호화된 컨텐츠 패키지{#package-encrypted-content}

1. 디렉토리를 로컬 파일 시스템에 `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 복사합니다.
1. 로컬 `Command Line Tools\` 폴더에서 서버에 사용할 파일을 업데이트합니다 `flashaccesstools.properties` .

   다음 속성 이상을 수정해야 합니다.

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`:라이센스 서버 인증서의 경로(일반적으로 [!DNL .cer]또는 [!DNL .der] 로 끝남) [!DNL .pem].

   * `encrypt.license.serverurl=[license-server-url]`:라이선스 서버 URL(예:   `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`Adobe

   * `encrypt.license.servercert=[transport-certificate.cer]`:전송 인증서의 경로(일반적으로 [!DNL .cer], [!DNL .der]또는 [!DNL .pem]로 끝남).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`:Packager 인증서 경로(다음으로 끝남) [!DNL .pfx].

   * `encrypt.sign.certpass=[password]`:Packager 인증서의 암호입니다.
   >[!NOTE]
   >
   >암호를 스크램블하지 않도록 하십시오.

1. 정책 만들기

   로컬 `Command Line Tools\` 폴더에서 다음 명령을 실행합니다.

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   이 명령은 익명 라이센스 서버 인증을 [!DNL examplepolicy.pol] 사용하는 정책 파일( `-x` 옵션)을 만듭니다.
1. 로컬 `Command Line Tools\` 폴더에 암호화할 MP4, FLV 또는 F4V 비디오 파일을 복사합니다.
1. 콘텐츠 패키징

   소스 비디오 파일이 [!DNL sample.mp4]있다고 가정해 봅시다. 로컬 `Command Line Tools\` 폴더에서 다음 명령을 실행합니다.

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >HLS, HDS 또는 대시 콘텐츠를 패키징하려면 Adobe Primetime Offline Packager와 같은 다른 패키지 [도구를 사용해야 합니다](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. 암호화된 파일 객체(이 경우 [!DNL sample_encrypted.mp4] 및 [!DNL sample_encrypted.mp4.metadata])를 에 `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`복사합니다.

이 시점에서 프로세스의 패키징 단계를 완료했습니다.

>[!NOTE]
>
>콘텐츠 패키징, 정책 제작 등을 위한 명령줄 도구에 대한 자세한 내용은 Adobe Primetime [DRM 명령줄 도구를](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md)참조하십시오.
