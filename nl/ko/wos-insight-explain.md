---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 트랜잭션 설명
{: #ie-ov}

각 배치에 대해 특정 트랜잭션에 대한 데이터의 설명 가능성을 볼 수 있습니다. 트랜잭션은 모니터를 지원하는 데이터가 있는 경우에만 나타나며 설정한 임계값, 모니터의 실행이 스케줄된 시간, {{site.data.keyword.pm_full}}에서 페이로드 데이터의 가용성을 기반으로 합니다.
{: shortdesc}

## 트랜잭션 ID별 설명 보기
{: #ie-view}

1. 배치 타일을 클릭하십시오. 
2. 네비게이터에서 **트랜잭션 설명** 탭(![트랜잭션 설명 탭](images/insight-transact-tab.png))을 클릭하십시오. 
3. 트랜잭션 ID를 입력하십시오. 

스코어링을 위해 모델에 데이터를 전송할 때마다 `X-Global-Transaction-Id` 필드를 설정하여 HTTP 헤더에 트랜잭션 ID를 설정해야 합니다. 이 트랜잭션 ID는 페이로드 테이블에 저장됩니다. 특정 스코어링에 대한 모델 동작의 설명을 찾으려면 해당 스코어링 요청과 연관된 트랜잭션 ID를 지정하십시오. 이 동작은 {{site.data.keyword.pm_full}} 트랜잭션에만 적용되며 비WML 트랜잭션에는 적용되지 않습니다.
{: note}

## {{site.data.keyword.aios_short}}에서 트랜잭션 ID 찾기
{: #ie-find}

1.  배치에 대한 시간 차트에서 마커를 차트를 가로질러 밀고 [특정 시간에 대한 데이터 시각화](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)에 대한 **세부사항 보기** 링크를 클릭하십시오.
1.  **트랜잭션 보기** 단추를 클릭하여 [트랜잭션 ID 목록을 보십시오](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  목록에서 트랜잭션 ID 중 하나를 복사하여 **트랜잭션 설명** 페이지의 검색 상자에 이를 붙여넣고 Enter를 누르십시오.

    임의의 트랜잭션 ID에 대한 조치 열에서 **설명** 링크를 클릭하는 방법으로도 트랜잭션 ID 목록을 표시할 수 있습니다. 이 경우, 설명 가능성 탭에서 트랜잭션이 열립니다.
    {: note}

  다른 유형의 모델에 대한 설명 예를 보려면 다음 절을 참조하십시오.

  ![설명 가능성 트랜잭션 ID](images/insight-explain-trans-id.png)

## 차트 세부사항을 통한 설명 찾기
{: #ie-view-ui}

설명이 공정성 및 드리프트 메트릭에 대해 존재하므로, 차트를 클릭하여 데이터 세트의 상세 보기를 가져온 후에 공정성 메트릭에 대해 **트랜잭션 보기** 단추를 클릭하거나 드리프트 트랜잭션 타일을 클릭하여 트랜잭션 설명을 볼 수 있습니다. 

- 성별 또는 나이 등의 공정성 속성 중 하나에 대해 속성을 클릭하고 차트를 클릭한 후 **트랜잭션 보기** 단추를 클릭하십시오. 
- 드리프트 모니터의 경우 **드리프트 규모**를 클릭하고 차트를 클릭한 후 타일을 클릭하여 해당 특정 드리프트 그룹과 연관된 트랜잭션을 보십시오. 

## 다음 단계
{: #ie-trans-id-next}

- [카테고리 모델 설명](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [이미지 모델 설명](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [비정형 텍스트 모델 설명](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [대조 설명](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
