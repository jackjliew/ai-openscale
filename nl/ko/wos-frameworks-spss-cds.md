---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: supported frameworks, models, model types, limitations, limits, spss, c&ds

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# IBM SPSS C&DS 프레임워크
{: #frmwrks-spss}

IBM SPSS C&DS를 사용하여 {{site.data.keyword.aios_full}}에서 페이로드 로깅, 피드백 로깅을 수행하고 성능 정확성, 런타임 편향성 감지, 설명 가능성 및 자동-편향성 함수를 측정할 수 있습니다. 

{{site.data.keyword.aios_full}}은 다음과 같은 IBM SPSS Collaboration and Deployment Services(C&DS) 프레임워크를 완전히 지원할 계획입니다.
{: shortdesc}

현재는 {{site.data.keyword.wos4d_full}}만 지원됩니다.
{: note}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| SPSS | 분류 | 구조 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

구독의 `deployment id`에 밑줄이 포함되어 있으면 공정성 메트릭의 편향성 제거된 탭에 일반적으로 표시되는 편향성 제거된 정확성이 표시되지 않습니다.
{: note}


## IBM SPSS Collaboration and Deployment Services(C&DS) 프레임워크에 대한 설명 가능성 지원
{: #frmwrks-spss-exp-supp}

- 설명 가능성은 모든 클래스의 확률을 리턴하는 SPSS 다중 클래스 모델과 2진 모델에 지원됩니다. 
- 설명 가능성은 우선하는 클래스 확률만 리턴하는 SPSS 다중 클래스 모델에는 지원되지 않습니다.



