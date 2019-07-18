---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted False Positive Rate, wFPR

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

# 加权假正率 (wFPR) ![beta 标记](images/beta.png)
{: #quality_wfpr_weighted}

加权假正率 (wFPR) 给出权重等于类概率的假正率 (FPR) 类的加权平均值。
{: shortdesc}

## 加权假正率 (wFPR) 概览
{: #quality_wfpr_weighted-glance}

- **描述**：权重等于类概率的类 FPR 的加权平均值
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：多类分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：混淆矩阵

## 解释显示内容
{: #quality_wfpr_weighted-display}

![显示加权假正率图表。](images/quality-fpr.png)

## 测算
{: #quality_wfpr_weighted-math}

加权假正率是使用加权数据的 FPR 的应用。

```
                   number of false positives
FPR =  ______________________________________________________

       (number of false positives + number of true negatives)
```
