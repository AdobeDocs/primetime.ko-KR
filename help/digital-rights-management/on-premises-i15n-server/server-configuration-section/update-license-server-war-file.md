---
title: 라이센스 서버 WAR 파일 업데이트
description: 라이센스 서버 WAR 파일 업데이트
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 라이센스 서버 WAR 파일 업데이트{#update-the-license-server-war-file}

온-프레미스 개별화 서버를 통해 개별화된 클라이언트를 지원하려면 새로 획득한 개별화 CA 자격 증명을 포함하도록 라이선스 서버의 인증서 루트를 업데이트해야 합니다. Python 스크립트( [!DNL addIndivCert.py])은 다음에 포함됩니다. [!DNL update_license_server] 폴더를 삭제합니다.

다음을 수행하여 라이센스 서버를 업데이트합니다.

1. 업데이트할 WAR 파일의 복사본을 만듭니다(예: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. WAR 파일이 잠금 해제되어 있고 수정할 수 있도록 해당 권한이 설정되어 있는지 확인하십시오.
1. 실행 [!DNL addIndivCert.py] 라이선스 서버 WAR 파일을 업데이트하는 Python 스크립트입니다.

   스크립트에 대한 입력은 다음과 같습니다.

   * `cert`: 개별화 CA 인증서가 포함된 PKCS12 파일
   * `war`: 업데이트할 WAR 파일

   출력 파일은 업데이트된 WAR 파일입니다.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

WAR 파일이 적절히 수정됩니다. 필요한 경우 특정 요구 사항에 맞게 Python 스크립트를 편집할 수 있습니다. 업데이트를 수행한 후 WAR 파일을 정상적으로 배포할 수 있습니다.
