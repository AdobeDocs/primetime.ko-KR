---
description: 사용자가 도메인 등록을 무시하기 위해 파일을 백업 및 복원하지 못하도록 하려면 일부 도메인 관리 접근 방식을 구현해야 합니다.
title: 도메인 관리
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 도메인 관리 {#managing-domains}

사용자가 도메인 등록을 무시하기 위해 파일을 백업 및 복원하지 못하도록 하려면 일부 도메인 관리 접근 방식을 구현해야 합니다.

다음은 도메인 관리 접근 방식입니다.

* 도메인 자격 증명이 유효한 시간을 제한합니다.

   자격 증명이 만료되면 클라이언트는 도메인 서버에 연결하여 도메인 자격 증명을 다시 받아야 합니다. 이때 도메인 서버는 컴퓨터가 여전히 도메인의 구성원임을 확인할 수 있습니다.
* 사용자가 등록을 취소할 때마다 도메인 키 위에 커서를 놓습니다.

   라이센스 서버는 최신 도메인 키가 있는 클라이언트에게만 라이센스를 발급해야 합니다. 이 방법에서는 라이센스 서버가 도메인 서버와 조정하여 최신 키를 알 수 있다고 가정합니다. 도메인 키를 롤오버하면 도메인에 대한 새 키 쌍이 생성됩니다. 도메인에 대한 키 위로 롤오버할 때 키 버전을 `generateDomainCredential`으로 증가시킵니다.
* 도메인 서버가 라이센스 서버와 동일한 경우 서버는 롤백 카운터를 사용하여 백업 및 복원을 감지할 수 있습니다.

   자세한 내용은 [Adobe Primetime DRM 요청 처리](../../protecting-content/implementing-the-license-server/processing-drm-requests.md)를 참조하십시오.

