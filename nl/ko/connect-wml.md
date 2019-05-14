---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Watson 기계 학습 서비스 인스턴스 지정
{: #wml-connect}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 Watson 기계 학습(WML) 인스턴스를 지정하는 것입니다. WML 인스턴스는 사용자의 AI 모델 및 배치를 저장하는 곳입니다.
{: shortdesc}

## 선행 조건
{: #wml-prereq}

{{site.data.keyword.aios_short}} 서비스 인스턴스가 있는 계정과 동일한 {{site.data.keyword.Bluemix_notm}} 계정에 프로비저닝된 WML 인스턴스가 있어야 합니다. 기타 계정에 프로비저닝된 WML 인스턴스가 있는 경우, {{site.data.keyword.aios_short}}을 사용하여 해당 인스턴스를 구성할 수 없습니다.

## Watson 기계 학습 서비스 인스턴스 연결
{: #wml-config}

{{site.data.keyword.aios_short}}은 WML 인스턴스에서 AI 모델 및 배치에 연결됩니다.

1.  {{site.data.keyword.aios_short}} 도구의 홈 페이지에서 **시작**을 클릭하십시오.

    ![홈 페이지](images/gs-config-start.png)

2.  Watson 기계 학습 타일을 선택하십시오.

    ![타일 선택](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}}이 사용자의 {{site.data.keyword.Bluemix_notm}} 계정을 확인하여 기존 WML 인스턴스를 찾습니다. 그런 다음 **Watson 기계 학습 서비스** 드롭 다운 메뉴에서 인스턴스를 선택할 수 있습니다.

    ![WML 서비스 선택](images/gs-set-wml.png)

4.  (선택사항) {{site.data.keyword.Bluemix_notm}} 계정 외부의 기계 학습 위치를 지정하려면 **다른 위치 선택**을 사용할 수 있습니다. 유효한 JSON으로 사용자의 위치에 대한 인증 정보를 제공하십시오.

    ![WML 인스턴스 설정](images/gs-get-wml.png)

    **다음**을 클릭하십시오.

5.  {{site.data.keyword.aios_short}}이 선택된 기계 학습 인스턴스를 검사하여 해당 인스턴스에 저장된 배치 목록을 찾습니다. 배치 목록에서 어느 것을 모니터링할 것인지 선택하십시오.

    ![배치 선택](images/gs-config-deploy.png)

6.  **다음**을 클릭하십시오.
7.  **저장**을 클릭하십시오.

### 다음 단계
{: #wml-next}

{{site.data.keyword.aios_short}}이 [데이터베이스를 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db)할 준비가 되었습니다.
