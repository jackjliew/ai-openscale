---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# 可解释方差的比例
{: #quality_var}

比例可释方差给出可释方差与目标方差的比率。“预期方差”是指目标方差与预测误差方差之间的差异。
{: shortdesc}

## 比例可释方差概览
{: #quality_var-glance}

- **描述**：“可解释方差的比例”是指可解释方差与目标方差之比。 “预期方差”是指目标方差与预测误差方差之间的差异。
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：回归
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：无

## 解释显示内容
{: #quality_var-display}

![显示比例可释方差图表。](images/xxxx.png)

## 测算
{: #quality_var-math}

通过对数字取平均值，然后为每个数字减去平均值并对结果取平方来计算比例可释方差。然后，计算出平方值

```
                                  sum of squares between groups 
Proportion explained variance =  ________________________________

                                      sum of squares total
```
