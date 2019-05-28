---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: accuracy, 

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

# 정확성
{: #acc-monitor}

정확성을 통해 모델이 결과를 얼마나 잘 예측하는지 알 수 있습니다.
{: shortdesc}

## 정확성 이해
{: #acc-understand}

정확성은 알고리즘의 유형에 따라 다른 것을 의미할 수 있습니다.

- *다중 클래스 분류*: 정확성이 임의의 클래스가 올바르게 예측할 수 있는 횟수를 측정하며 데이터 점의 수로 정규화됩니다. 자세한 정보는 Apache Spark 문서에서 [다중 클래스 분류 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window}를 참조하십시오.

- *2진 분류*: 2진 분류 알고리즘의 경우, 정확성이 ROC 곡선 아래의 영역으로 측정됩니다. 자세한 정보는 Apache Spark 문서에서 [2진 분류 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window}를 참조하십시오.

- *회귀*: 회귀 알고리즘은 결정 계수 또는 R2를 사용하여 측정됩니다. 자세한 정보는 Apache Spark 문서에서 [회귀 모델 평가 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window}를 참조하십시오.

### 작동 방식
{: #acc-works}

[Python 클라이언트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} 또는 [Rest API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window}을 사용하여 아래 표시되는 {{site.data.keyword.aios_short}} UI를 통해 수동으로 레이블링된 피드백 데이터를 추가해야 합니다.

정확성 모니터링 제한사항은 [지원되는 프레임워크](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)를 검토하십시오.

<!---
You need to add manually-labelled data into your feedback table for the accuracy computation to trigger. The feedback table is in the posgres schema with the name <model_id>_feedback.

You can create a performance monitoring system for your predictive models by creating an evaluation instance, and then defining the metrics and triggers for the automatic retraining and deploying of the new model. Spark, Keras and TensorFlow models are supported at this stage, with the following requirements:

- A training definition must be stored in the repository
- `training_data_reference` - must be defined as a part of the stored model's metadata
- `training_definition_url` - must be defined as a part of the stored model's metadata

Use the available [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-ml-api.mybluemix.net/){: new_window} end-points directly to provide feedback data and kick off evaluation activities. For more information, see the [WML documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/ml-continuous-learning.html?audience=wdp&context=wdp){: new_window}.
--->

## 정확성 모니터 구성
{: #acc-config}

1.  *정확성의 개념* 페이지에서 **다음**을 클릭하여 구성 프로세스를 시작하십시오.

    ![정확성의 개념 페이지](images/accuracy-what-is.png)

1.  *정확성 임계값 설정* 페이지에서 허용 가능한 정확성 레벨을 나타내는 값을 선택하십시오.

    정확성은 각 특정 모델 유형과 연관된 관련 데이터 사이언스 메트릭으로부터 합성된 값입니다. 스코어는 다른 모델 유형 전체에 걸쳐 정확성을 쉽게 비교할 수 있게 해주는 정규화된 측도입니다. 일반적인 상황에서는 정확성 스코어가 80이면 충분합니다.
    {: note}

    ![정확성 한계 설정](images/accuracy-set-limit.png)

    **다음**을 클릭하여 계속하십시오.

1.  이제 최소 및 최대 샘플 크기를 설정하십시오. 최소 값은 평가 데이터 세트에서 최소 수의 레코드가 사용 가능할 때까지 정확성 측정을 금지합니다. 이로 인해 샘플 크기가 너무 작아서 결과를 왜곡시키는 것을 방지할 수 있습니다. 최대 샘플 크기는 크기가 초과되는 경우에 최신 레코드만 평가되도록 하여 데이터 세트를 평가하는 데 드는 시간과 노력을 더 잘 관리할 수 있도록 돕습니다.

     ![샘플 크기 구성](images/accuracy-config-sample.png)

1.  **다음** 단추를 클릭하십시오.

    검토를 위해 선택사항 요약이 표시됩니다. 변경해야 할 사항이 있으면 해당 섹션의 **편집** 링크를 클릭하십시오.

1.  **저장**을 클릭하여 구성을 완료하십시오.

이제 정확성을 평가하기 위해 모델에 직접 피드백 데이터를 제공할 수 있는 옵션이 표시됩니다.

  ![피드백 데이터 전송](images/accuracy-send-feedback0.png)

*피드백 데이터 추가* 단추를 선택하여 CSV 형식의 데이터 파일을 업로드하십시오. 이 때, 데이터에 적합한 구분 기호를 설정하십시오. 

피드백 CSV 파일에는 모든 특성 값 및 수동으로 지정된 대상/레이블 값이 있을 것으로 예상됩니다. 예를 들어, 약제 모델 훈련 데이터는 `"AGE"`, `"SEX"`, `"BP"`, `"CHOLESTEROL"`, `"NA"`, `"K"` 등의 특성 값과 `"DRUG"` 대상/레이블 값을 포함합니다. 피드백 CSV 파일은 해당 필드에 대한 값을 포함해야 합니다. 예를 들어, 예제가 `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`와 같이 표시될 것입니다. 피드백 CSV 파일에 대해 헤더가 제공되면 헤더를 사용하여 필드 이름이 맵핑됩니다. 그렇지 않으면 필드 순서가 교육 스키마에서와 완전히 **동일해야** 합니다. 훈련 데이터에 대한 자세한 정보는 [{{site.data.keyword.aios_short}}에서 내 훈련 데이터에 액세스해야 하는 이유는 무엇입니까?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)를 참조하십시오.
{: important}

모델에 의해 리턴되는 예측 유형 및 피드백 데이터의 레이블/대상 열이 일치해야 합니다.
{: note}

  ![정확성 구분 기호](images/accuracy-delimit.png)

파일 크기는 현재 8MB로 제한됩니다.
{: note}

또는 제공된 `cURL` 또는 `Python` 코드 스니펫을 사용하여 피드백 데이터를 공개할 수 있습니다.

코드 스니펫에 제공되는 필드 및 값은 예이므로 이를 사용자의 실제 값으로 대체해야 합니다.
{: important}

또한 **종료**를 선택하여 이 선택적 단계를 건너뛸 수 있습니다. 나중에 평가에 필요한 CSV 파일을 업로드할 수 있습니다.

### 다음 단계
{: #acc-next}

*모니터 구성* 페이지에서 다른 모니터링 카테고리를 선택할 수 있습니다.
