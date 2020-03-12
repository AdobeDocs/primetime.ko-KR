---
seo-title: 라이센스 서버 WAR 파일 업데이트
title: 라이센스 서버 WAR 파일 업데이트
uuid: 0cde53d6-185d-4bf2-84fc-0c31d17904a8
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# 라이센스 서버 WAR 파일 업데이트{#update-the-license-server-war-file}

온-프레미스 개인화 서버를 통해 개인화된 클라이언트를 지원하려면 새로 취득한 개인화 CA 자격 증명을 포함하려면 라이센스 서버의 인증서 신뢰 루트를 업데이트해야 합니다. Python 스크립트( [!DNL addIndivCert.py])가 [!DNL update_license_server] 폴더에 포함되어 있습니다.

라이센스 서버를 업데이트하려면 다음을 수행합니다.

1. 업데이트할 WAR 파일의 복사본을 만듭니다(예:( [!DNL flashaccess.war]으) [!DNL faxsks.war]).
1. WAR 파일의 잠금을 해제하고 권한을 설정하여 수정할 수 있는지 확인합니다.
1. Python [!DNL addIndivCert.py] 스크립트를 실행하여 License Server WAR 파일을 업데이트합니다.

   스크립트의 입력은 다음과 같습니다.

   * `cert`:개인화 CA 인증서를 포함하는 PKCS12 파일
   * `war`:업데이트할 WAR 파일
   출력 파일은 업데이트된 WAR 파일입니다.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

WAR 파일은 제자리에서 수정됩니다. 필요한 경우 Python 스크립트를 특정 요구 사항에 맞게 편집할 수 있습니다. 업데이트를 수행한 후 WAR 파일을 정상적으로 배포할 수 있습니다.
