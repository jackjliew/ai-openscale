---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# ROC 下的面积 ![beta 标记](images/beta.png)
{: #quality_roc}

接收者操作特征曲线下的面积给出查全率和假正率曲线下的面积。它针对错检率计算敏感度。
{: shortdesc}

## ROC 下的面积概览
{: #quality_roc-glance}

- **描述**：查全率曲线和误报率曲线下的面积
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：二元分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：混淆矩阵

## 解释显示内容
{: #quality_roc-display}

![显示 ROC 下的面积图表。](images/quality-area-under-roc.png)

## 测算
{: #quality_roc-math}

ROC 下的面积按照阈值 `T` 以参数化方式绘制为`真正率`与`误报率`的比较。



