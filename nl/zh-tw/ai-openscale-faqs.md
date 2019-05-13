---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: FAQs, frequently asked questions, questions

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# 常見問題 (FAQ)
{: #wos-faqs}

您可以在這裡找到來自 {{site.data.keyword.aios_full}} 使用者的一些常見問題。
{: shortdesc}

## 問題
{: #wos-faqs-questions}

- [如何將預測直欄從整數資料類型轉換成種類資料類型？](#wos-faqs-convert-data-types)

### 如何將預測直欄從整數資料類型轉換成種類資料類型？
{: #wos-faqs-convert-data-types}

在配置模型的公平性監視時，預測直欄只接受整數值，即使預測標籤是種類也一樣。如何針對種類特性（亦即，不是整數）來配置此項？需要手動轉換嗎？ 

訓練資料可能有 "Loan Denied"、"Loan Granted" 等之類的類別標籤。WML 評分端點所傳回的預測值會是 "0.0"、"1.0" 等之類的值。評分端點也有一個選用直欄，其中含有以文字表示的預測。例如，如果 prediction=1.0，則 predictionLabel 直欄的值可能是 "Loan Granted"。如果這類直欄是可用的，則在配置模型的有利和不利輸出結果時，您可以指定字串值 "Loan Granted" 和 "Loan Denied"。如果這類直欄無法使用，則對於有利/不利類別，需要指定整數/倍精準數值 1.0、0.0。

WML 具有輸出綱目概念，藉以定義 WML 評分端點輸出的綱目，以及不同直欄的角色。這些角色用來識別哪個直欄含有預測值，哪個直欄含有預測機率，以及類別標籤值等。輸出綱目會自動設定給使用模型建置器建立的模型。此外，也可以使用 WML Python 用戶端來設定它。使用者可以使用輸出綱目，來定義含有以字串表示之預測的直欄。其作法是將直欄的 modeling_role 設為 'decoded-target'。WML Python 用戶端的相關說明文件位於：http://wml-api-pyclient-dev.mybluemix.net/#repository。搜尋 "OUTPUT_DATA_SCHEMA"，以瞭解輸出綱目和 store_model API，此 API 可接受以 OUTPUT_DATA_SCHEMA 作為參數。



