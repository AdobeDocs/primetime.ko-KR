---
title: 암호화된 콘텐츠 패키지
description: 암호화된 콘텐츠 패키지
copied-description: true
exl-id: e5792917-8172-48b0-8792-7a7e942596c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 암호화된 콘텐츠 패키지{#package-encrypted-content}

1. 다음을 복사합니다. `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` 로컬 파일 시스템에 대한 디렉토리입니다.
1. 로컬 `Command Line Tools\` 폴더, 업데이트 `flashaccesstools.properties` 서버에서 사용할 파일입니다.

   최소한 다음 속성을 수정해야 합니다.

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: 라이선스 서버 인증서 경로(일반적으로 다음으로 끝남) [!DNL .cer], [!DNL .der] 또는 [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: 라이선스 서버 URL입니다. 예:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: 전송 인증서에 대한 경로(일반적으로 다음으로 끝남) [!DNL .cer], [!DNL .der], 또는 [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: Packager 인증서 경로(다음으로 끝남) [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: Packager 인증서의 암호입니다.
   >[!NOTE]
   >
   >암호를 스크램블하지 않는지 확인합니다.

1. 정책을 만듭니다.

   로컬 `Command Line Tools\` 폴더에서 다음 명령을 실행합니다.

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   이 명령은 이름이 인 정책 파일을 만듭니다. [!DNL examplepolicy.pol] 익명 라이선스 서버 인증을 사용하는 `-x` 선택 사항).
1. 암호화할 MP4, FLV 또는 F4V 비디오 파일을 로컬에 복사합니다. `Command Line Tools\` 폴더를 삭제합니다.
1. 콘텐츠를 패키징합니다.

   소스 비디오 파일이 [!DNL sample.mp4]. 로컬 `Command Line Tools\` 폴더에서 다음 명령을 실행합니다.

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >HLS, HDS 또는 DASH 컨텐츠를 패키징하려면 다음과 같은 다른 packager 도구를 사용해야 합니다. [Adobe Primetime 오프라인 패키지](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. 암호화된 파일 아티팩트 복사(이 경우 [!DNL sample_encrypted.mp4] 및 [!DNL sample_encrypted.mp4.metadata]) 받는 사람 `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

이 시점에서 프로세스의 패키징 단계를 완료했습니다.

>[!NOTE]
>
>콘텐츠 패키징, 정책 만들기 등을 위한 명령줄 도구에 대한 자세한 내용은 [Adobe Primetime DRM 명령줄 도구](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
