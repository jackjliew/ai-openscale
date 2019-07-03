---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: databases, connections, scoring, requests, schema, REST API, API

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

# 사용자 정의 기계 학습 엔진 예
{: #fmrk-workaround-cstmmlsengex}

다음 예를 사용하여 고유 사용자 정의 기계 학습 엔진을 설정하십시오.
{: shortdesc}

## Python 및 Flask
{: #fmrk-workaround-pandflask}

[git에 공개된 사용자 정의 ML 엔진 예](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)에서는 python과 flask를 사용하여 scikit-learn 모델에 서비스를 제공합니다.

[README 파일](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)에서는 IBM Cloud의 cf 애플리케이션 외에도 테스트용으로 앱을 로컬에 배치하는 방법을 설명합니다. REST API 엔드포인트의 구현은 [app.py 파일](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py)에 있습니다.

## Node.js
{: #fmrk-workaround-nodejs}

[여기에는 Node.js](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs)로 작성된 사용자 정의 기계 학습 엔진의 예도 있습니다.

## End2end 코드 패턴
{: #fmrk-workaround-e2ecode}

{{site.data.keyword.aios_short}}와의 통합 및 사용자 정의 엔진 배치에 관한 end2end 예를 보여주는 [코드 패턴](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale).

