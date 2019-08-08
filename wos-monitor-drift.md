---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, drift, configuration, monitors

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

# Configuring the drift detection monitor ![beta tag](images/beta.png)
{: #behavior-drift-config}

You must configure the {{site.data.keyword.aios_full}} drift monitor before it can begin to analyze your model. You can train your model online by using the {{site.data.keyword.aios_full}} user interface or by using a notebook.
{: shortdesc}

You can train your model online by using {{site.data.keyword.aios_short}}
if you use {{site.data.keyword.pm_full}} and your data does not exceed 500 MB. Otherwise, you must use a notebook to train the model.

## Requirements
{: #behavior-drift-config-steps-wos-reqs}

Throughout this process, {{site.data.keyword.aios_full}} analyzes your model and makes recommendations based on the most logical outcome. On the successive pages of the **Drift** tab, you must provide the following information:

### Alert threshold
{: #behavior-drift-config-steps-wos-reqs-alert}

{{site.data.keyword.aios_full}} tracks the degree of change in model accuracy when compared to accuracy at training time. The alert threshold, which must be at least 5%, indicates the degree of tolerance for change over time.

### Sample size
{: #behavior-drift-config-steps-wos-reqs-sample}

By setting a minimum sample size, you prevent measuring drift until a minimum number of records are available in the evaluation dataset. This ensures the sample size is not too small to skew results. Every time drift checking runs, it will use the minimum sample size to decide the number of records on which it will do the computation.

## Steps to configure drift in {{site.data.keyword.aios_short}}
{: #behavior-drift-config-steps-wos}

If you use {{site.data.keyword.pm_full}}, you have the option of using the {{site.data.keyword.aios_short}} user interface to configure drift detection.

1. From the **Drift** tab, on the **What is Drift**? page, click **Begin** to start the configuration process.

   ![What is Drift? page](images/wos-drift-config-1.png)

2. Click the **Train in Watson OpenScale** tile.

   ![What is Drift? page](images/wos-drift-config-1a.png)

5. Follow the prompts and enter required information. When you finish, a summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section, otherwise, save your work.

## Steps to configure drift without retraining
{: #behavior-drift-config-steps-no-training}

Reconfigure the drift monitor without re-training the drift model to update parameters without performing additional processing. You might do this to update the minimum sample size and threshold to produce more data on the currently trained model without incurring additional processing costs. It is one way to avoid intensive CPU usage when the underlying data hasn't changed and you only want to view drift magnitude with different thresholds. Drift model retraining is only required when training data or schema has changed.

1. From the **Drift** tab, on the **What is Drift**? page, click **Begin** to start the configuration process.

   ![What is Drift? page](images/wos-drift-config-1.png)

2. Click **Edit** and then click the **Use the existing drift model** tile.

   ![What is Drift? page](images/drift-config-2.png)

5. Follow the prompts and enter required information. When you finish, a summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section, otherwise, save your work.



## Steps to configure drift using a notebook
{: #behavior-drift-config-steps-ntbk}

If you use a machine learning provider other than {{site.data.keyword.pm_full}}, such as Microsoft Azure, Amazon SageMaker, or a custom machine learning engine you must use a notebook to configure drift detection. It is possible to configure drift for {{site.data.keyword.pm_full}} by using this method, as well.

This option is useful if the training data is not stored in Db2 or {{site.data.keyword.cos_full}}. Using a notebook, you must read the training data into a dataframe. The specialized notebook that you can download from {{site.data.keyword.aios_short}} then creates a specialized output that you can upload to {{site.data.keyword.aios_short}}.

1. Create a notebook to generate the drift detection model. Use [the sample notebook](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external} that is available from the {{site.data.keyword.aios_short}} UI.
2. Use compression software to compress the drift detection model into a .tar.gz file.

1. From the **Drift** tab, on the **What is Drift**? page, click **Begin** to start the configuration process.

   ![What is Drift? page](images/wos-drift-config-1.png)

2. Click the **Train in a notebook** tile.

   ![What is Drift? page](images/wos-drift-config-1a.png)

3. Drag the compressed model file into the target zone, or browse to select it and click **Next**.

   ![What is Drift? page](images/wos-drift-config-2b.png)
   
3. Upload the drift detection model and click **Next**.

   ![What is Drift? page](images/drift-config-upload.png)
   
5. Follow the prompts and enter required information. When you finish, a summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section, otherwise, save your work.

## Next steps
{: #behavior-drift-config-next-steps}

- For more information about interpreting drift, see [Drift magnitude](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)