---
title: ECI 파일 정보
description: ECI 파일 정보
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# ECI 파일 정보{#about-eci-files}

CRL 외에도 ECI(Embedded Common Interface) 파일을 정기적으로 업데이트해야 합니다. Adobe이 새로운 Primetime DRM 클라이언트 플랫폼에 대한 지원을 추가할 때마다(예:iOS, Android, Windows FlashPlayer 등)에서 새 ECI 레코드가 만들어집니다. 이 클라이언트의 개별화를 지원하려면 해당 ECI 레코드가 Indification Server에 있어야 합니다.

새로운 Primetime DRM 클라이언트는 빈번하지 않으므로 Adobe은 필요에 따라 업데이트된 ECI 데이터를 출시할 예정입니다. Adobe은 주기적으로 ECI 파일을 수집하여 배포하기 위해 아래 위치에 호스트합니다.

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

[!DNL Latest.txt] 파일에는 가장 최근 CRL 배포 파일의 URL이 포함됩니다.

Adobe은 아래 설명된 방법으로 ECI zip 파일을 만듭니다.

폴더 구조:

```
ECI\*
```

폴더의 내용이 재귀적으로 압축됩니다.

```
zip -R ECI ECI.zip
```

OpenSSL SHA-256 다이제스트는 zip 파일에 대해 계산됩니다.

```
openssl dgst -sha256 -hex ECI.zip
```

zip 파일의 이름은 SHA-256 다이제스트뿐만 아니라 아카이브 날짜를 포함하는 것으로 변경됩니다.

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

예:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

업데이트된 ECI 파일이 있는지 위 위치를 정기적으로 확인해야 합니다.

다운로드 후 설치 과정을 수행합니다.

1. SHA-256 다이제스트를 확인하고 OpenSSL 또는 이와 동등한 도구를 사용하여 다시 계산합니다.
1. 파일 이름에 지정된 것과 비교합니다.
1. 파일 이름을 [!DNL ECI.zip]으로 변경합니다.
1. [!DNL ECI] 디렉토리의 압축을 해제합니다.
1. 이전 ECI 디렉토리를 새 디렉토리로 바꿉니다.
1. 개인화 서버를 다시 시작합니다.

