---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: deployment, monitors, data

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

# 배치에 대한 모니터 준비
{: #mo-config}

{{site.data.keyword.aios_short}}을 사용하여 추적하고 있는 각 배치에 대해 모니터를 설정하고 사용 가능하도록 설정하십시오.
{: shortdesc}

## 배치 선택
{: #mo-select-deploy}

1.  먼저, 배치를 선택해야 합니다.

    지정된 모델에 대해 여러 배치가 있는 경우에 하나의 배치를 구성하면 동일한 모델에 대한 기타 모든 배치도 구성됩니다.
    {: note}

    ![배치 선택 페이지](images/config-select-deploy.png)

1.  *모니터링 준비* 타일을 선택하십시오.

    ![모니터링 준비](images/config-prep-monitor.png)

## 데이터에 대해 작업
{: #mo-work-data}

1.  이제 모델 및 교육 데이터에 대한 정보를 제공합니다. **다음**을 클릭하십시오.

    ![설명 준비](images/config-what-monitor.png)

1.  드롭 다운 메뉴에서 배치가 분석할 데이터 유형을 선택하고 **다음**을 클릭하십시오.

    ![입력 유형 선택](images/config-input-monitor.png)

### 숫자/카테고리 데이터
{: #mo-nuca}

숫자 또는 카테고리 데이터의 경우, 모니터를 구성하려면 모델에 대한 교육 데이터에 대한 정보를 제공해야 합니다.

  ![구성 유형 선택](images/config-manual-monitor.png)

- **수동으로 모니터 구성** - 교육 데이터에 대한 연결 정보를 제공하도록 요구합니다.

    - [알고리즘 유형](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)을 선택하고 **다음**을 클릭하십시오.

      ![다중 클래스](images/multiclass.png)

      교육 데이터의 형식이 모델이 예상하는 형식과 정확하게 일치하는지 확인하십시오. 예를 들어, 모델이 *Gender*특성으로 `M` 및 `F`를 예상하면 교육 데이터가 `Male` 및 `Female`이 아니라 `M` 및 `F`여야 합니다. 현재 {{site.data.keyword.aios_short}}은 Db2 데이터베이스 또는 Cloud Object Storage 위치만 지원합니다.
        {: important}

    - 위치(`Db2` 또는 `Cloud Object Storage`)를 지정하고 다음을 수행하십시오.

        - Db2 데이터베이스의 경우, 다음을 완료하십시오.

            - 호스트 이름 또는 IP 주소
            - 포트
            - 데이터베이스(이름)
            - 사용자 이름
            - 비밀번호

            ![교육 데이터 페이지의 Db2 위치 지정](images/config-train-db2-monitor.png)

        - Cloud Object Storage의 경우, 다음을 완료하십시오.

            - 로그인 URL

              로그인 URL은 사용자의 교육 데이터가 위치하는 버킷의 영역 설정과 일치해야 합니다. 다음 단계에서 교육 데이터 버킷을 지정합니다.
              {: important}

            - 리소스 인스턴스(ID)
            - API 키

            ![교육 데이터의 Cloud Object Storage 위치 지정 페이지](images/config-train-cos-monitor.png)

    - 교육 데이터에 연결하려면 **테스트** 단추를 클릭하여 유효한 연결인지 확인하십시오. **다음**을 클릭하십시오.

    - 교육 데이터가 위치한 Db2 데이터베이스 또는 Cloud Object Storage의 정확한 위치를 지정하십시오.

        - Db2 데이터베이스의 경우, 모델에 필요한 열을 포함하는 스키마 및 교육 테이블을 둘 다 선택하십시오.

          ![스키마 및 교육 테이블의 Db2 위치 지정](images/fair-config-table-db2.png)

        - Cloud Object Storage의 경우, 버킷 및 데이터 세트를 선택하십시오.

          ![데이터 세트의 Cloud Object Storage 위치 지정](images/fair-config-dset-cos.png)

          **다음**을 클릭하여 아래의 5단계로 진행하십시오.

- **구성 파일 업로드** - 교육 데이터를 개인용으로 유지하려면 이 옵션을 선택하십시오. 사용자 정의 Python Notebook을 사용하면 교육 데이터 자체에 대한 액세스를 제공하지 않고도 교육 데이터를 분석하는 데 필요한 정보를 {{site.data.keyword.aios_short}}에 제공할 수 있습니다.

  Python Notebook을 실행하면 열 이름 및 스키마 열 내의 구분 값을 캡처할 수 있습니다. 또한 Notebook을 사용하여 공정성 모니터를 사전 구성할 수 있습니다.

    - [사용자 정의 Notebook ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: new_window}을 다운로드하여 모든 인증 정보를 사용자 자신의 인증 정보로 대체하십시오.

    - 적절한 모델용 데이터를 지정하면서 Notebook을 주의 깊게 검토하십시오. Notebook을 저장하십시오.

    - Notebook을 실행하여 JSON 형식의 구성 파일을 생성하십시오.

    - JSON 구성 파일을 업로드하십시오.

        ![구성 JSON 업로드](images/config-json-monitor.png)

    - **다음**을 클릭하십시오.

- {{site.data.keyword.aios_short}}이 WML의 모델을 사용하여 저장된 메타데이터에서 교육 데이터를 찾습니다. 예측 값을 포함하는 교육 데이터에서 레이블 열을 선택하고 **다음**을 클릭하십시오.

  ![열 레이블 선택](images/fair-config-column.png)

- 모델을 훈련시키는 데 사용되는 열을 선택하십시오. 이는 모델 배치가 요청에서 예상하는 특성입니다. **다음**을 클릭하십시오.

    ![열 레이블 선택](images/explain-select-column.png)

- 마지막으로 텍스트를 포함하였다가 정수로 변환된 열을 선택하십시오. 예를 들어, 원래 교육 데이터는 *Gender*에 대해 `Male` 및 `Female`을 포함했으나 지금은 `0` 및 `1`에 각각 맵핑되었으며 이제 교육 데이터가 *Gender* 열에 대해 `0` 및 `1` 값을 포함합니다. 우, 원래 포함된 텍스트 값이 아니라 정수를 포함하는 열을 식별하십시오. **다음**을 클릭하십시오.

    ![데이터 테이블 선택](images/explain-text-column.png)

### 이미지 및 비정형 텍스트
{: #mo-imun}

- **이미지**

  이미지를 입력으로 허용하는 모델의 경우, 이미지가 (높이) x (너비) x (# 채널) 형식으로 다시 표시되어야 합니다. 이 때, 각 점은 각 픽셀에 대한 흑백 또는 RGB 값을 나타냅니다.

- **비정형 텍스트**

   텍스트를 입력으로 허용하는 모델의 경우, 모델이 텍스트의 벡터화된 표현이 아니라 전체 텍스트를 허용할 것으로 예상됩니다.

## 구성 검토 및 저장
{: #mo-save}

선택 요약을 검토하고 **저장**을 클릭하여 계속하십시오.

  ![데이터 테이블 선택](images/config-summary-monitor.png)

### 다음 단계
{: #mo-next}

모니터 구성을 시작하려면 카테고리를 선택하고 **시작**을 클릭하십시오.
