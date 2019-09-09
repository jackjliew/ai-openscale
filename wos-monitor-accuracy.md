---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

keywords: accuracy, 

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

# Configuring the quality monitor
{: #acc-monitor}

The quality monitor (previously known as the accuracy monitor) lets you know how well your model predicts outcomes.
{: shortdesc}

## Requirements
{: #acc-config-reqs}

On the successive pages of the **Quality** tab, you must provide the following information:

### Quality alert threshold

Select a value that represents an acceptable accuracy level. For example, if you are using the **German Credit Risk model** for the interactive tutorial, set the alert to **90%**.

Quality is a value synthesized from relevant data science metrics associated with each particular model type. The score is a normalized measure to allow you to easily compare accuracy across different model types. In typical situations, an accuracy score of 80 is sufficient. For the tutorial, to generate more data, we recommend 90.
{: note}

### Minimum and maximum sample sizes

By setting a minimum sample size, you prevent measuring quality until a minimum number of records are available in the evaluation dataset. This ensures the sample size is not too small to skew results. Every time quality checking runs, it will use the minimum sample size to decide the number of records on which it will do the quality metrics computation.

The maximum sample size helps better manage the time and effort it takes to evaluate the dataset. Only the most recent records are evaluated if this size is exceeded. For example, if you are using the **German Credit Risk model** for the interactive tutorial, set the minimum sample size to **100** and the maximum sample size to **10000**.

## Steps
{: #acc-config}

To start the configuration process, from the **Quality** tab, on the **What the Quality monitor?** page, click **Begin**.

![The What is the Quality monitor? page is shown and it explains that the quality monitor evaluates how well you model predicts accurate outcomes](images/wos-quality-what-is.png)

Follow the prompts and enter required information. When you finish, a summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section, otherwise, save your work.

A summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section. Otherwise, click **Save** to complete your configuration.

### Next steps
{: #acc-next}

To continue configuring monitors, click the **Fairness** tab and click **Begin**. For more information, see [Configuring the fairness monitor](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
