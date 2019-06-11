---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 사용자 정의 모니터 및 메트릭 작성 ![베타 태그](images/beta.png)
{: #cst_mtrcs}

사용자 정의 모니터는 양적 방식으로 모델 배치 및 비즈니스 애플리케이션의 요소를 추적할 수 있는 사용자 정의 메트릭 세트가 통합되어 있습니다. 사용자 정의 메트릭을 정의할 수 있으며, 모델 품질, 성능 또는 {{site.data.keyword.aios_full}}에서 모니터링되는 공정성 메트릭과 같은 표준 메트릭과 함께 사용할 수 있습니다.
{: shortdesc}

사용자 정의 모니터 및 메트릭을 관리하려면, Python SDK의 일부인 프로그램 인터페이스를 사용해야 합니다. 유사한 방식으로 {{site.data.keyword.aios_short}} 데이터 마트에 사용자 정의 메트릭을 저장하여 필요할 때 액세스할 수 있습니다. 사용자 정의 메트릭은 {{site.data.keyword.aios_short}} 대시보드에도 표시됩니다.

## 사용자 정의 메트릭 관리
{: #cst_mtrc_mgmt}

사용자 정의 메트릭에 대해 작업하려면 다음 태스크를 수행해야 합니다.

1. 메트릭 정의와 함께 사용자 정의 모니터를 등록하십시오.
2. 사용자 정의 모니터를 사용으로 설정하십시오.
3. 메트릭 값을 저장하십시오.

다음의 고급 튜토리얼에서는 이를 수행하는 방법을 보여줍니다.

- [Watson Machine Learning에 대한 작업](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [사용자 정의 기계 학습 엔진에 대한 작업](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

언제든지 사용자 정의 모니터링을 사용 및 사용 안함으로 설정할 수 있습니다. 더 이상 필요하지 않게 되면 사용자 정의 모니터를 제거할 수 있습니다.

자세한 정보는 [Python SDK 문서](http://ai-openscale-python-client.mybluemix.net/)를 참조하십시오.

## 사용자 정의 메트릭 액세스 및 시각화
{: #cst_mtrcs_viz}

사용자 정의 메트릭에 액세스하고 시각화하기 위해 프로그램 인터페이스를 사용할 수 있습니다. 다음의 고급 튜토리얼에서는 이를 수행하는 방법을 보여줍니다.

- [Watson Machine Learning에 대한 작업](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [사용자 정의 기계 학습 엔진에 대한 작업](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   자세한 정보는 [Python SDK 문서](http://ai-openscale-python-client.mybluemix.net/)를 참조하십시오.

고객 메트릭의 시각화는 {{site.data.keyword.aios_short}} 대시보드에 표시됩니다.

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
