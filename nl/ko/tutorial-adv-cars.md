---

title: Trust and transparency for your machine learning models with {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 튜토리얼(고급)
{: #tadv-tutorial-advanced}

## 시나리오
{: #tadv-scenario}

자동차 렌트 회사가 고객 만족도에 대한 피드백 데이터를 수집했습니다. 제시된 모델은 이 데이터를 사용하여 다음 렌트에 사용할 수 있는 쿠폰을 제공하는 것과 같이 고객을 확보하기 위한 일련의 조치를 예측합니다.

모델은 고객 데이터 필드 ID(ID 번호), GENDER, STATUS(미혼 또는 기혼), CHILDREN(수), AGE, CUSTOMER STATUS(활성 또는 비활성), CAR OWNER(예 또는 아니오), CUSTOMER SERVICE(고객 주석), SATISFACTION(만족 또는 불만족) 및 BUSINESS AREA(제품 또는 서비스 관련)를 사용하여 ACTION 데이터 필드에 대한 네 값(해당사항 없음, 쿠폰, 무료 업그레이드, 요청 시 픽업) 중 하나를 예측합니다.

## 선행 조건
{: #tadv-prereqs}

이 튜토리얼을 완료하려면 다음이 필요합니다.

- [Watson Studio ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://dataplatform.ibm.com/){: new_window} 계정
- [{{site.data.keyword.cloud_notm}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}){: new_window} 계정

튜토리얼을 수행하는 동안 다음과 같은 Lite(무료) {{site.data.keyword.cloud_notm}} 서비스를 프로비저닝합니다.

- 기계 학습
- Apache Spark
- Object Storage

또한 다음과 같은 **유료** {{site.data.keyword.cloud_notm}} 서비스를 프로비저닝합니다.

- PostgreSQL

  신용카드를 사용하여 유료 계정으로 전환하는 것으로 $200 {{site.data.keyword.cloud_notm}} 신용을 얻을 수 있습니다. 이미 유료 계정인 경우, 한 달 동안 첫 GB의 스토리지에 대해 일회의 $16 요금 환불을 받을 수 있습니다.
  {: tip}

PostgreSQL 데이터베이스 및 Watson Machine Learning 인스턴스가 동일한 {{site.data.keyword.cloud_notm}} 계정에 배치되어야 합니다.
{: important}

필수 서비스를 이미 프로비저닝한 경우, 예를 들어, 기타 튜토리얼을 완료한 경우, 아래의 [Watson Studio 프로젝트](#tadv-setup-ws)로 진행하십시오.

## 소개
{: #tadv-intro}

이 튜토리얼에서는 다음과 같이 학습합니다.

- {{site.data.keyword.cloud_notm}} 기계 학습 및 스토리지 서비스를 프로비저닝합니다.
- Watson Studio 프로젝트를 설정하고 Python Notebook을 실행하여 기계 학습 모델을 작성, 교육 및 배치합니다.
- Python Notebook을 실행하여 데이터 마트를 작성하고 성능, 정확성 및 공정성 모니터를 구성하고 모니터할 데이터를 작성합니다.
- {{site.data.keyword.aios_short}} 인사이트 탭에서 결과를 봅니다.

## {{site.data.keyword.cloud_notm}} 서비스 프로비저닝
{: #tadv-svcs}

IBM ID로 [{{site.data.keyword.cloud_notm}} 계정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}){: new_window}에 로그인하십시오. 서비스를 프로비저닝할 때, 특히 Apache Spark, Object Storage 및 Db2 Warehouse의 경우, 선택된 조직 및 공간이 모든 서비스에 대해 동일한지 확인하십시오.

### Watson Studio 계정 작성
{: #tadv-stac}

- 아직 계정과 연관된 인스턴스가 없으면 [Watson Studio 인스턴스를 작성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/watson-studio){: new_window}하십시오.

  ![Watson Studio](images/watson_studio.png)

- 서비스에 이름을 지정하고 Lite(무료) 플랜을 선택한 다음 **작성** 단추를 클릭하십시오.

### 기계 학습 서비스 프로비저닝
{: #tadv-pml}

- 아직 계정과 연관된 인스턴스가 없으면 [Watson Machine Learning 인스턴스를 프로비저닝 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/machine-learning){: new_window}하십시오.

  ![기계 학습](images/machine_learning.png)

- 서비스에 이름을 지정하고 Lite(무료) 플랜을 선택한 다음 **작성** 단추를 클릭하십시오.

- 기계 학습 서비스 인증 정보를 기록해 두십시오. 사용자의 기계 학습 인스턴스에서 페이지 왼쪽의 **서비스 인증 정보** 링크를 클릭하십시오. 인증 정보의 이름을 지정하고 **추가**를 클릭하십시오. 그런 다음 인증 정보 목록에서 **인증 정보 보기**를 클릭하고 나중에 사용할 수 있도록 인증 정보를 복사하십시오.

### Spark 서비스 프로비저닝
{: #tadv-ps}

- 아직 계정과 연관된 서비스가 없으면 [Spark 서비스를 프로비저닝 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/apache-spark){: new_window}하십시오.

  ![Apache Spark](images/spark.png)

- 서비스에 이름을 지정하고 Lite(무료) 플랜을 선택한 다음 **작성** 단추를 클릭하십시오.

- Spark 인스턴스의 서비스 인증 정보를 기록해 두십시오. Spark 인스턴스를 열고 왼쪽 메뉴에서 **서비스 인증 정보**를 클릭하십시오. **새 인증 정보** 단추를 클릭하고 인증 정보의 이름을 지정한 다음 **추가**를 클릭하십시오. 그런 다음 방금 작성한 세트 바로 옆의 **인증 정보 보기** 링크를 클릭하고 나중에 사용할 수 있도록 인증 정보를 복사하십시오.

### Object Storage 서비스 프로비저닝
{: #tadv-pos}

- 아직 계정과 연관된 서비스가 없으면 [Object Storage 서비스를 프로비저닝 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window}하십시오.

  ![Object Storage](images/object_storage.png)

- 서비스에 이름을 지정하고 Lite(무료) 플랜을 선택한 다음 **작성** 단추를 클릭하십시오.

### 유료 PostgreSQL 서비스 프로비저닝
{: #tadv-ppgs}

- 아직 계정과 연관된 서비스가 없으면 [유료 PostgreSQL 서비스를 프로비저닝 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window}하십시오.

  ![Compose for PostgreSQL](images/postgres.png)

- 서비스에 이름을 지정하고 표준 플랜을 선택한 다음 **작성** 단추를 클릭하십시오.

  신용카드를 사용하여 유료 계정으로 전환하는 것으로 $200 {{site.data.keyword.cloud_notm}} 신용을 얻을 수 있습니다. 이미 유료 계정인 경우, 한 달 동안 첫 GB의 스토리지에 대해 일회의 $16 요금 환불을 받을 수 있습니다.
  {: tip}

- PostgreSQL 인스턴스의 서비스 인증 정보를 기록해 두십시오. 기존 또는 새로 작성한 PostgreSQL 인스턴스를 열고 왼쪽 메뉴에서 **서비스 인증 정보**를 클릭하십시오. **새 인증 정보** 단추를 클릭하고 인증 정보의 이름을 지정한 다음 **추가**를 클릭하십시오. 그런 다음 방금 작성한 세트 바로 옆의 **인증 정보 보기** 링크를 클릭하고 나중에 사용할 수 있도록 인증 정보를 복사하십시오.

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![수동으로 데이터 유형 설정](images/data-type-manual.png)

- 훈련 데이터가 열에 올바르게 표시되어야 합니다. 계속하려면 **다음**을 클릭한 다음 **로드 시작**을 클릭하여 데이터를 로드하십시오.

--->

## Watson Studio 프로젝트 설정
{: #tadv-setup-ws}

- [Watson Studio 계정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://dataplatform.ibm.com/){: new_window}에 로그인하십시오. 상단 오른쪽에서 계정 아바타 아이콘을 클릭하고 사용 중인 계정이 {{site.data.keyword.cloud_notm}} 서비스를 작성할 때 사용한 계정과 동일한지 확인하십시오.

  ![동일한 계정](images/same_account.png)

- Watson Studio에서 새 프로젝트를 작성하여 시작하십시오. "프로젝트 작성"을 선택하십시오.

  ![Watson Studio 프로젝트 작성](images/studio_create_proj.png)

- **표준** 타일을 선택하여 프로젝트를 작성하십시오.

  ![Watson Studio 표준 프로젝트 선택](images/studio_create_standard.png)

- 프로젝트에 이름과 설명을 지정하고 이전 단계에서 작성한 Object Storage 서비스가 **스토리지** 드롭 다운에서 선택되어 있는지 확인하고 **작성**을 클릭하십시오.

### {{site.data.keyword.cloud_notm}} 서비스와 Watson 프로젝트 연관시키기
{: #tadv-acsw}

- Watson Studio 프로젝트를 열고 **설정** 탭을 선택하십시오. **연관된 서비스** 섹션에서 **서비스 추가** 드롭 다운을 클릭하고 **Watson**을 선택하십시오:

  ![Watson 서비스 추가](images/add_watson_service.png)

- **기계 학습** 타일에서 **추가** 링크를 클릭하고 **기존** 탭을 선택하십시오. **기존 서비스 인스턴스** 드롭 다운에서 이전 섹션에서 작성한 서비스를 선택하고 **선택**을 클릭하십시오.

- 프로젝트 설정 탭에서 **서비스 추가**를 다시 선택하고 드롭 다운에서 **Spark**를 선택하십시오. **기존** 탭에서 사용자가 작성한 Spark 서비스를 선택하고 **선택**을 클릭하십시오.

## 기계 학습 모델 작성 및 배치
{: #tadv-deploy-ml}

### Watson Studio 프로젝트에 `CARS4U Action Recommendation - model` Notebook 추가

- 다음 파일을 다운로드하십시오.

    - [CARS4U Action Recommendation - model ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- Watson Studio 프로젝트의 **자산** 탭에서 **프로젝트에 추가** 단추를 클릭하고 드롭 다운에서 **Notebook**을 선택하십시오.

  ![연결 추가](images/add_notebook.png)

- **파일에서**를 선택하십시오.

  ![새 Notebook 양식](images/new_notebook_name.png)

- 그런 다음 **파일 선택** 단추를 클릭하고 다운로드한 "CARS4U Action Recommendation - model"을 선택하십시오.

  ![새 Notebook 양식](images/new_notebook_name2.png)

- **런타임 선택** 섹션의 드롭 다운 목록에서 이전에 작성한 Spark 인스턴스를 선택하십시오.

  ![Spark 런타임](images/spark_runtime.png)

- **Notebook 작성**을 클릭하십시오.

### `CARS4U Action Recommendation - model` Notebook 편집 및 실행
{: #tadv-ern}

`CARS4U Action Recommendation - model` Notebook에는 사용자가 실행할 python 코드 내의 각 단계에 대한 자세한 지침이 포함되어 있습니다. Notebook을 통해 실행하면서 각 명령이 수행하는 내용에 대해 이해하는 것이 중요합니다.
{: tip}

- Watson Studio 프로젝트의 **자산** 탭에서 `CARS4U Action Recommendation - model` Notebook 옆의 **편집** 아이콘을 클릭하여 이를 편집하십시오.

- 섹션 2.2, "PostgreSQL 데이터베이스로 데이터 업로드"에서 Postgres 서비스 인증 정보를 이전 섹션에서 사용자가 작성한 인증 정보로 대체하십시오.

- 섹션 4, "저장소에 모델 저장"의 **팁** 아래에서 Watson Machine Learning 인증 정보를 이전 섹션에서 사용자가 작성한 인증 정보로 대체하십시오.

- 일단 인증 정보를 입력했으면 Notebook을 실행할 준비가 된 것입니다. **커널** 메뉴 항목을 클릭하고 메뉴에서 **다시 시작 및 모두 실행**을 선택하십시오.

  ![다시 시작 및 실행](images/restart_and_run.png)

  프로젝트에서 **CARS4U - Action Recommendation Model**을 작성하고 교육하며 배치합니다. Watson Studio 프로젝트의 **배치** 탭을 선택하고 **CARS4U - Area and Action Model Deployment** 링크를 클릭하여 모델이 배치되었는지 확인할 수 있습니다.

## {{site.data.keyword.aios_short}} 구성
{: #tadv-config-aios}

### {{site.data.keyword.aios_short}} 프로비저닝
{: #tadv-paios}

- {{site.data.keyword.aios_short}}의 인스턴스를 아직 프로비저닝하지 않았으면 {{site.data.keyword.cloud_notm}} 계정에서 **카탈로그** 링크를 클릭하여 "OpenScale"을 필터링하십시오. {{site.data.keyword.aios_short}}에 대한 타일을 선택하십시오.

<!---
  ![{{site.data.keyword.aios_short}}](images/openscale.png)
--->

- 서비스에 이름을 지정하고 Lite 플랜을 선택한 다음 **작성**을 클릭하십시오.

### {{site.data.keyword.aios_short}}을 기계 학습 모델에 연결
{: #tadv-cmlm}

이제 기계 학습 모델이 배치되었으므로 모델의 신뢰성 및 투명성을 보장하도록 {{site.data.keyword.aios_short}}을 구성할 수 있습니다. {{site.data.keyword.aios_short}} 인스턴스의 **관리** 탭을 선택하고 **애플리케이션 시작** 단추를 클릭하십시오. {{site.data.keyword.aios_full}} 시작하기 페이지가 열립니다. **시작**을 클릭하십시오.

- "Watson Machine Learning" 타일을 선택하고 **다음**을 클릭하십시오.

  ![WML 인스턴스 설정](images/gs-wml-default.png)

- 드롭 다운에서 Watson Machine Learning 인스턴스를 선택하고 **다음**을 클릭하십시오.

  ![WML 인스턴스 설정](images/gs-set-wml.png)

- 이제 {{site.data.keyword.aios_short}}이 모니터할 배치된 모델을 선택할 수 있습니다. 작성하여 배치한 모델을 선택하고 **다음**을 클릭하여 이를 승인하십시오.

  ![배치된 모델 선택](images/gs-set-deploy.png)

- 이제 PostgreSQL 데이터베이스를 선택해야 합니다. 두 가지 옵션, 즉, 무료 Lite 플랜 데이터베이스 및 기존 또는 신규 데이터베이스가 있습니다. 이 튜토리얼의 경우, **기존 데이터베이스 사용 또는 새 데이터베이스 구매** 타일을 선택하십시오.

    ![데이터베이스 선택](images/gs-set-lite-db1.png)

[데이터베이스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db) 주제에서 이러한 각 옵션에 대한 전체 세부사항을 볼 수 있습니다.
  {: note}

- 일단 "기존 데이터베이스 사용 또는 신규 데이터베이스 구매" 옵션을 선택하면 {{site.data.keyword.aios_short}}이 사용자의 {{site.data.keyword.cloud_notm}} 계정을 확인하여 기존 Compose for PostgreSQL 데이터베이스를 찾습니다.

 **스키마** 드롭 다운 메뉴에서 "data_mart" 스키마를 선택하십시오.

  ![데이터베이스 선택](images/gs-set-schema1.png)

- 일단 데이터베이스 및 스키마를 선택하였으면 **다음**을 클릭하여 요약 데이터를 검토하고 **저장**을 클릭하십시오.

  ![데이터베이스 선택](images/gs-setup-summary3.png)

  프롬프트가 표시되면 **종료 후 대시보드로 이동**을 클릭하십시오.

## 데이터 마트 작성 및 성능, 정확성 및 공정성 모니터 구성
{: #tadv-config-monitors}

### Watson Studio 프로젝트에 `{{site.data.keyword.aios_short}} and Watson ML engine` Notebook 추가
{: #tadv-aomn}

`{{site.data.keyword.aios_short}} and Watson ML engine` Notebook에는 사용자가 실행할 python 코드 내의 각 단계에 대한 자세한 지침이 포함되어 있습니다. Notebook을 통해 실행하면서 각 명령이 수행하는 내용에 대해 이해하는 것이 중요합니다.
{: tip}

- 다음 파일을 다운로드하십시오.

    - [{{site.data.keyword.aios_short}} and Watson ML engine ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Watson Studio 프로젝트의 **자산** 탭에서 **프로젝트에 추가** 단추를 클릭하고 드롭 다운에서 **Notebook**을 선택하십시오.

  ![연결 추가](images/add_notebook.png)

- **파일에서**를 선택하십시오.

  ![새 Notebook 양식](images/new_notebook_name.png)

- 그런 다음 **파일 선택** 단추를 클릭하고 다운로드한 "{{site.data.keyword.aios_short}} and Watson ML engine"을 선택하십시오.

  ![새 Notebook 양식](images/new_notebook_name3.png)

- **런타임 선택** 섹션의 드롭 다운 목록에서 이전에 작성한 Spark 인스턴스를 선택하십시오.

  ![Spark 런타임](images/spark_runtime.png)

- **Notebook 작성**을 클릭하십시오.

### `{{site.data.keyword.aios_short}} and Watson ML engine` Notebook 편집 및 실행
{: #tadv-eromn}

- Watson Studio 프로젝트의 **자산** 탭에서 `{{site.data.keyword.aios_short}} and Watson ML engine` Notebook 옆의 **편집** 아이콘을 클릭하여 이를 편집하십시오.

- 섹션 1.1, "설치 및 인증":

    - **조치: instance_id(GUID) 및 apikey 가져오기** 아래의 인증 정보를 가져오기 위한 지침을 따르십시오. `aios_credentials`를 자신의 인증 정보로 대체하십시오.

    - 다음으로 **조치: 여기에 Watson Machine Learning 인증 정보 추가**에서 Watson Machine Learning 인증 정보를 사용자가 앞에서 작성한 인증 정보로 대체하십시오.

    - 마지막으로 **조치: 여기에 PostgreSQL 인증 정보 추가** 아래에서 Postgres 인증 정보를 사용자가 앞에서 작성한 인증 정보로 대체하십시오.

- 일단 인증 정보를 입력했으면 Notebook을 실행할 준비가 된 것입니다. **커널** 메뉴 항목을 클릭하고 메뉴에서 **다시 시작 및 모두 실행**을 선택하십시오.

  ![다시 시작 및 실행](images/restart_and_run.png)

  그러면 데이터 마트가 설정되고 페이로드 로깅을 사용할 수 있도록 설정되며 성능, 정확성 및 공정성 모니터를 구성하고 스코어링할 수 있으며 이러한 메트릭을 {{site.data.keyword.aios_short}} 인스턴스에 제공할 수 있습니다.

## 결과 보기
{: #tadv-results}

### 배치에 대한 인사이트 보기
{: #tadv-vide}

[{{site.data.keyword.aios_short}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}를 사용하여 **인사이트** 탭을 클릭하십시오.

  ![인사이트](images/insight-dash-tab.png)

인사이트 페이지에서 배치된 모델에 대한 메트릭 개요를 볼 수 있습니다. Notebook을 실행할 때 설정한 임계값(70%) 아래로 떨어진 공정성 또는 정확성 메트릭에 대한 경보를 쉽게 볼 수 있습니다. 이 튜토리얼에서 사용된 데이터와 설정은 여기에서 표시된 정확성 및 공정성과 유사한 메트릭을 갖게 됩니다.

  ![인사이트 개요](images/insight-overview-adv-tutorial.png)

### 배치에 대한 모니터링 데이터 보기
{: #tadv-vmdd}

인사이트 페이지에서 타일을 클릭하여 배치를 선택하십시오. 배치에 대한 모니터링 데이터가 표시됩니다. 마커를 차트를 가로질러 밀어서 Notebook을 실행한 동안의 시간 프레임에 대한 데이터를 선택하십시오. 그런 다음 **세부사항 보기** 링크를 선택하십시오.

  ![모니터 데이터](images/insight-monitor-data1.png)

이제 모니터한 데이터에 대한 차트를 검토할 수 있습니다. 이 예의 경우, **특성** 드롭 다운을 사용하여 "Children" 또는 "Gender"를 선택하여 모니터되는 데이터에 대한 세부사항을 보십시오.

  ![인사이트 개요](images/insight-review-charts1.png)

<!---

### 모델 트랜잭션에 대한 설명 가능성 보기
{: #tadv-vemt}

모니터할 데이터에 대한 차트에서 **트랜잭션 보기** 단추를 선택하십시오.

  ![View transactions](images/view_transactions.png)

  지난 시간 동안 트랜잭션의 목록이 나열됩니다. 트랜잭션 ID 중 하나를 복사하십시오.

  ![Transaction list](images/transaction_list.png)

Using the [{{site.data.keyword.aios_short}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, click on the **Explainability** tab:

  ![Explainability](images/explainability.png)

복사한 트랜잭션 ID를 검색 상자에 붙여넣고 키보드에서 **Return**을 누르십시오. 모델의 신뢰도, 신뢰수준에 기여한 요인 및 모델에 공급된 열을 포함하여 모델이 결론에 이르게 된 방법을 설명합니다.

  ![View Transaction](images/view_transaction1.png)

--->

## 다음 단계
{: #tadv-next}

- [데이터 보기 및 해석](/docs/services/ai-openscale?topic=ai-openscale-it-ov) 및 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)에 대해 자세히 알아보십시오.
