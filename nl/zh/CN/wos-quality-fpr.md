---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# 误报率 (FPR)
{: #quality_fpr_false}

假正率给出不正确预测在正类中的比例。
{: shortdesc}

## 误报率 (FPR)
{: #quality_fpr_false-glance}

- **描述**：正类中不正确预测的比例
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在恶化。反馈数据正在变得明显不同于训练数据。
   - **下降趋势**：下降趋势表明度量正在改善。 这意味着，模型再训练是有效的。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：二元分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：混淆矩阵

## 解释显示内容
{: #quality_fpr_false-display}

![显示假正率图表。](images/quality-fpr.png)

## 测算
{: #quality_fpr_false-math}

假正率的计算方式是，先计算假正的数量加上真负的数量之和，再用假正总数除以和。

```
                        number of false positives
False positive rate =  ______________________________________________________

                       (number of false positives + number of true negatives)
```
