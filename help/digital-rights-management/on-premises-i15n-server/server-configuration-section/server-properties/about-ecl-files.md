---
seo-title: ECI 파일 정보
title: ECI 파일 정보
uuid: 124d8ab1-933b-4a1b-992a-919f3d799460
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# ECI 파일 정보{#about-eci-files}

CRL 외에 ECI(Embedded Common Interface) 파일도 정기적으로 업데이트해야 합니다. Adobe가 새로운 Primetime DRM 클라이언트 플랫폼에 대한 지원을 추가할 때마다(예:iOS, Android, Windows FlashPlayer 등)에 새 ECI 레코드가 만들어집니다. 이 클라이언트의 개별화를 지원하려면 해당 ECI 레코드가 Indification Server에 있어야 합니다.

새로운 Primetime DRM 클라이언트의 릴리스가 매우 빈번하지 않으므로 Adobe는 필요에 따라 업데이트된 ECI 데이터를 제공할 것입니다. Adobe는 정기적으로 ECI 파일을 수집하여 배포하기 위해 아래 위치에 호스팅합니다.

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

이 [!DNL Latest.txt] 파일에는 최신 CRL 배포 파일에 대한 URL이 포함됩니다.

Adobe는 아래 설명된 방법으로 ECI zip 파일을 만듭니다.

폴더 구조:

```
ECI\*
```

폴더의 컨텐츠가 반복적으로 압축됩니다.

```
zip -R ECI ECI.zip
```

zip 파일에 대해 OpenSSL SHA-256 다이제스트가 계산됩니다.

```
openssl dgst -sha256 -hex ECI.zip
```

zip 파일의 이름은 SHA-256 다이제스트뿐만 아니라 아카이브 날짜를 포함하도록 변경됩니다.

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

예:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

위의 위치에 업데이트된 ECI 파일이 있는지 정기적으로 확인해야 합니다.

다운로드 후 설치 과정을 수행합니다.

1. SHA-256 다이제스트를 확인하고 OpenSSL 또는 이와 동등한 도구를 사용하여 다시 계산합니다.
1. 파일 이름에 지정된 것과 비교합니다.
1. 파일 이름을 바꿀 [!DNL ECI.zip]수 있습니다.
1. 디렉토리 압축을 [!DNL ECI] 해제합니다.
1. 이전 ECI 디렉토리를 새 디렉토리로 바꿉니다.
1. 개인화 서버를 다시 시작합니다.

