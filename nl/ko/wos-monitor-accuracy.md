---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# 품질(정확성) 모니터 구성
{: #acc-monitor}

품질 모니터(이전에는 정확성 모니터라고 함)를 통해 모델이 결과를 얼마나 잘 예측하는지를 알 수 있습니다.
{: shortdesc}

## 구성 단계
{: #acc-config}

**품질** 탭의 **품질 모니터의 개념** 페이지에서 **시작**을 클릭하여 구성 프로세스를 시작하십시오.

![품질 모니터의 개념 페이지가 표시되며, 이는 모델이 정확한 결과를 예측하는 수준을 품질 모니터가 평가함을 설명합니다. ](images/wos-quality-what-is.png)

정확성 구성 탭의 이후 페이지에서 다음 설정을 구성하십시오.

-  정확성 경보 임계값을 설정하십시오. 허용 가능한 정확성 레벨을 나타내는 값을 선택하십시오. 예를 들어, 대화식 튜토리얼의 경우 **독일 신용 위험 모델**을 사용 중이면 경보를 다음으로 설정하십시오. **90%**.

    정확성은 각 특정 모델 유형과 연관된 관련 데이터 사이언스 메트릭으로부터 합성된 값입니다. 스코어는 다른 모델 유형 전체에 걸쳐 정확성을 쉽게 비교할 수 있게 해주는 정규화된 측도입니다. 일반적인 상황에서는 정확성 스코어가 80이면 충분합니다. 튜토리얼의 경우 추가 데이터를 생성하려면 90을 권장합니다.
    {: note}

-  최소 및 최대 샘플 크기를 설정하십시오. 최소 값은 평가 데이터 세트에서 최소 수의 레코드가 사용 가능할 때까지 정확성 측정을 금지합니다. 이로 인해 샘플 크기가 너무 작아서 결과를 왜곡시키는 것을 방지할 수 있습니다. 최대 샘플 크기는 크기가 초과되는 경우에 최신 레코드만 평가되도록 하여 데이터 세트를 평가하는 데 드는 시간과 노력을 더 잘 관리할 수 있도록 돕습니다. 예를 들어, 대화식 튜토리얼의 경우 **독일 신용 위험 모델**을 사용 중이면 최소 샘플 크기를 **100**으로 설정하고 최대 샘플 크기를 **10000**으로 설정하십시오. 


검토를 위해 선택사항 요약이 표시됩니다. 변경해야 할 사항이 있으면 해당 섹션의 **편집** 링크를 클릭하십시오. 그렇지 않은 경우 **저장**을 클릭하여 구성을 완료하십시오.

### 다음 단계
{: #acc-next}

모니터 구성을 계속하려면 **공정성** 탭을 클릭한 후 **시작**을 클릭하십시오. 자세한 정보는 [공정성 모니터 구성](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)을 참조하십시오. 
