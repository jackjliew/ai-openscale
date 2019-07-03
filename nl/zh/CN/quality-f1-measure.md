---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, F1-Measure

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

# F1 度量 ![beta 标记](images/beta.png)
{: #quality_f1-measr}

F1 度量给出查准率和查全率的调和均值。
{: shortdesc}

## F1 度量概览
{: #quality_f1-measr-glance}

- **描述**：精度和查全率的调和均值
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：二元分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：混淆矩阵

## 解释显示内容
{: #quality_f1-measr-display}

![显示 F1 度量图表。](images/quality-f1-meas.png)

## 测算
{: #quality_f1-measr-math}

F1 度量是查准率和查全率的加权调和平均值或均值。

```
          (precision * recall)
F1 = 2 *  ____________________

          (precision + recall)
```
