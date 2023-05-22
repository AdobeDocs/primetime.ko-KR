---
title: 교차 도메인 정책 파일
description: 교차 도메인 정책 파일
copied-description: true
exl-id: dbe16692-cdf7-4a91-9303-8afc2d487112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 교차 도메인 정책 파일 {#crossdomain-policy-file}

라이선스 서버가 비디오 재생 SWF이 아닌 다른 도메인에서 호스팅되는 경우 SWF이 라이선스 서버에서 라이선스를 요청할 수 있도록 하려면 도메인 간 정책 파일(crossdomain.xml)이 필요합니다. 도메인 간 SWF 파일은 서버에서 해당 데이터와 문서를 다른 도메인에서 제공되는 정책 파일에 사용할 수 있음을 나타내는 방법을 제공하는 XML 파일입니다. 라이선스 서버의 도메인 간 SWF 파일에 지정된 도메인에서 제공되는 모든 정책 파일은 해당 라이선스 서버의 데이터 또는 에셋에 액세스할 수 있습니다.

Adobe은 개발자가 도메인 간 정책 파일을 배포할 때 신뢰할 수 있는 도메인만 라이선스 서버에 액세스하도록 허용하고 웹 서버의 라이선스 하위 디렉터리에 대한 액세스를 제한하여 모범 사례를 따를 것을 권장합니다.

도메인 간 정책 파일에 대한 자세한 내용은 다음 위치를 참조하십시오.

* 웹 사이트 컨트롤(정책 파일)
* 도메인 간 정책 파일 사양: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
