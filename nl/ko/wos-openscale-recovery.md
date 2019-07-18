---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# 고가용성 및 재해 복구
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}}은 댈러스 및 워싱턴 DC 등의 다중 {{site.data.keyword.cloud_notm}} 위치에서 가용성이 매우 높습니다. 그러나 전체 위치에 영향을 주는 잠재적인 재해에서 복구하려면 계획 및 준비가 필요합니다.
{: shortdesc}

서비스의 구성, 사용자 정의 및 사용법을 이해하는 것은 사용자의 책임입니다. 또한 새 위치에서 서비스의 인스턴스를 새로 작성할 수 있도록 준비하고 데이터를 임의의 위치에서 복원하는 것도 사용자의 책임입니다. 자세한 정보는 [작동 중단이 발생하지 않도록 하는 방법](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external}을 참조하십시오.

## 고가용성 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}}은 세 개의 가용성 구역에 MZR(Multiple Zone Routing)이 있는 **미국 남부** 데이터 센터에서 배치되고 사용 가능합니다. 언제든 하나의 구역을 사용할 수 없는 경우 시스템은 기타 가용성 구역에서 계속 사용 가능합니다. 글로벌 로드 밸런서 및 DNS 서버가 사용자 개입 없이 사용 가능한 구역으로 트래픽을 라우팅합니다.

PostgreSQL 데이터베이스에 저장되는 데이터 또한 가용성이 높으며 다중 가용성 구역에 존재합니다. 단, 서비스가 다시 작성될 수 있도록 재해 복구 계획을 지원하여 데이터를 백업하는 것은 사용자의 책임입니다.

{{site.data.keyword.aios_short}} 트래픽은 영역 내의 다중 구간 전체에 걸쳐 로드 밸런스됩니다. 각 구역은 동일한 영역 내의 데이터 센터입니다. 

PostgreSQL 등의 Compose 데이터베이스 및 분산된 <code>etc</code> 디렉토리(etcd) 데이터베이스는 재해가 발생하는 경우에 고가용성을 보장하고 {{site.data.keyword.aios_short}} 운영 팀이 RPO(Recovery Point Objective) 내에 서비스를 복구할 수 있도록 정기적으로 백업됩니다.
 
{{site.data.keyword.cloud_notm}}는 고가용성 보호를 가능하게 하는 영역 내 중복성을 제공합니다. IBM은 추가 비용 없이 교육 및/또는 사용자 정의 모델 데이터를 포함하여 클라이언트 데이터베이스에 대한 자동 데이터 복제를 제공합니다. 복제는 {{site.data.keyword.cloud_notm}} 데이터 센터 내의 영역 내 가용성 구역 전체에 대해 완료됩니다.
 
## 백업 및 복원
{: #openscale-restore}

고객은 고객이 권한을 부여한 사용자 정의 모델 및 교육 및/또는 사용자 정의 모델 데이터를 포함하여 자신의 데이터를 백업하고 복원할 책임이 있습니다. 고객 백업 및 복원 지침에 대한 정보는 {{site.data.keyword.cloud_notm}} 문서를 참조하십시오.
 
## 재해 복구
{: #openscale-disaster-recovery}

영역 내 비즈니스 연속성은 {{site.data.keyword.cloud_notm}} 데이터 센터 내의 영역 내 가용성 구역 전체에 대한 자동 복제를 활용하여 완료됩니다. 고객은 다중 영역 재해 복구에 대한 책임이 있습니다. 이러한 책임에는 고객이 생성한 사용자 정의 모델, 자체 보안 정책 및 교육 및/또는 사용자 정의 모델 데이터의 백업,복원 및 동기화가 포함됩니다. 또한 영역 전체에 걸친 라우팅 및 로드 밸런싱에도 책임이 있습니다. 고객 백업 및 복원 지침에 대한 정보는 {{site.data.keyword.cloud_notm}} 문서를 참조하십시오.
