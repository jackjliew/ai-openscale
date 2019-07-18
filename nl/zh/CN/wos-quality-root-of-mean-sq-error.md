---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 均方根误差 ![beta 标记](images/beta.png)
{: #supqualdets_squ_errors_mean}

均方根误差 (RMSE) 视图显示模型中的预测值与观察值之间的差值。
{: shortdesc}

## 均方根误差概览
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **描述**：模型预测值与目标值之间平方差平均值的平方根
- **缺省阈值**：上限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在恶化。反馈数据正在变得明显不同于训练数据。
   - **下降趋势**：下降趋势表明度量正在改善。 这意味着，模型再训练是有效的。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：回归
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：无

## 解释显示内容
{: #supqualdets_squ_errors_mean-display}

![显示均方根误差图表。](images/xxxx.png)

## 测算
{: #supqualdets_squ_errors_mean-math}

均方根误差等于（预测减去观察值）平方的平均值的平方根。

```
          ___________________________________________________________
RMSE  =  √(forecasts - observed values)*(forecasts - observed values)
```
