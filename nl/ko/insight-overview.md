---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 대시보드 탐색
{: #io-ov}

{{site.data.keyword.aios_short}} 대시보드를 통해 모니터링하고 있는 모든 배치를 추적할 수 있습니다. 대시보드는 {{site.data.keyword.aios_short}}에 대한 기본 보기입니다. 대시보드는 다섯 개 탭으로 구성됩니다.

  ![인사이트 탭](images/insight-tabs.png)

{: shortdesc}

## 인사이트
{: #io-ins}

**인사이트** 탭(![인사이트 대시보드](images/insight-dash-tab.png))은 배치 모니터링의 상위 레벨 보기를 제공합니다.

  ![인사이트 대시보드](images/insight-dashboard.png)

- ***모니터링되는 배치*** - 이 예에서 총 10개의 배치가 모니터됩니다. 10개의 배치 중 8개가 아래의 개별 타일로 표시됩니다.

- ***정확성 경보*** - 총 3개의 정확성 경보가 보라색 그림자로 아래 타일에 표시됩니다. 이 예에서, `Driver Performance`, `Market Analytics` 및 `Pricing Risk` 배치의 정확성 값이 각각 `60%`, `65%`, 및 `79%` 로 표시됩니다.

- ***공정성 경보*** - 총 6개의 공정성 경보가 있으며 보라색 그림자 및 작은 `BIAS` 태그로 아래 타일에 표시됩니다. 이 예에서 `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization` 및 `Damage Cost Estimator` 배치의 공정성 값이 각각 `59%`, `68%`, `62%`, `64%`, `79%`, 및 `63%` 로 표시됩니다.

각 타일이 해당 배치에 대한 모니터링 활동의 요약을 제공합니다. `Call Center Routing` 배치 타일은 매우 안정적이며 정확한 모델을 표시하며 문제가 있어 보이지 않습니다.

### 다음 단계
{: #io-next}

개별 배치 타일 중 하나를 선택하여 해당 배치에 대한 세부사항을 볼 수 있습니다. 자세한 정보는 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-it-ov) 및 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.

## 구성
{: #io-conf}

**구성** 탭(![구성 탭](images/insight-config-tab.png))은 선택된 배치에 대한 구성 요약을 엽니다.

  ![구성 요약](images/insight-config-summary.png)

여기서부터, 직접 배치 모니터에 대한 구성 설정을 편집할 수 있습니다.

## 트랜잭션
{: #io-tran}

**트랜잭션 설명** 탭(![트랜잭션 설명 탭](images/insight-transact-tab.png))을 사용하면 특정 배치 트랜잭션을 설명할 특정 트랜잭션 ID를 검색할 수 있습니다. 자세한 정보는 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.

## AI 도구
{: #io-too}

**AI 도구** 탭(![AI 도구 탭](images/aitools.png))은 추가 IBM AI 도구 옵션에 대한 링크를 제공하는 대화 상자를 엽니다.

- *[Watson Studio Lite 플랜 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*: Watson Studio는 데이터를 분석하고 시각화하거나, 정리하고 구성하거나, 스트리밍 데이터를 수집하는 데 필요한 도구, 또는 기계 학습 모델을 작성하고, 교육하고, 배치하는 데 필요한 환경 및 도구를 제공합니다. "무료 Watson Studio Lite 플랜에 등록" 링크를 클릭하면 Watson Studio로 이동합니다.

- *[NeuNetS ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}*(*Beta*): Neural Network Synthesizer 또는 "NeuNetS"는 현재 베타 릴리스 상태이며 Watson Studio에서 {{site.data.keyword.aios_short}} 기술을 사용하여 AI 모델을 합성할 수 있습니다. NeuNetS로 작업하려면 "모델 합성"을 클릭하십시오.

  ![NeuNetS 대화 상자](images/neunets-dialog.png)

## 도움말 탭
{: #io-help}

도움말 탭(![트랜잭션 탭](images/insight-help-tab.png))은 {{site.data.keyword.aios_short}} 사용을 지원하기 위한 추가 정보를 제공합니다.
