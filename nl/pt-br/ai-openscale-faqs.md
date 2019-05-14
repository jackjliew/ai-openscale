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

# Perguntas Frequentes
{: #wos-faqs}

Aqui, você encontrará algumas das perguntas mais frequentes de usuários do {{site.data.keyword.aios_full}}.
{: shortdesc}

## Dúvidas
{: #wos-faqs-questions}

- [Como eu converto uma coluna de predição de um tipo de dados de número inteiro em um tipo de dados categórico?](#wos-faqs-convert-data-types)

### Como eu converto uma coluna de predição de um tipo de dados de número inteiro em um tipo de dados categórico?
{: #wos-faqs-convert-data-types}

Ao configurar o monitoramento de justiça para um modelo, a coluna de predição permite somente um valor numérico inteiro mesmo que o rótulo de predição seja categórico. Como configurar isso para o recurso categórico (que não é um número inteiro)? é necessária uma conversão manual? 

Os dados de treinamento podem ter rótulos de classe, como “Loan Denied”, “Loan Granted”. O valor prediction retornado pelo terminal de pontuação do WML tem valores como “0.0”, “1.0" etc. O terminal de pontuação também tem uma coluna opcional que contém a representação de texto da predição. Por exemplo, se prediction=1.0, a coluna predictionLabel poderia ter um valor “Loan Granted”. Se essa coluna estiver disponível, enquanto estiver configurando o resultado favorável e desfavorável para o modelo, será possível especificar os valores de sequência “Loan Granted” e “Loan Denied”. Se essa coluna não estiver disponível, será necessário especificar os valores de número inteiro/duplo de 1.0, 0.0 para a classe favorável/desfavorável.

O WML tem um conceito de esquema de saída que define o esquema da saída do terminal de pontuação do WML e a função para as colunas diferentes. As funções são usadas para identificar qual coluna contém o valor prediction, qual coluna contém a probabilidade de predição e o valor do rótulo de classe etc. O esquema de saída é configurado automaticamente para modelos criados usando o construtor de modelo. Isso também pode ser configurado usando o cliente python do WML. Os usuários podem usar o esquema de saída para definir uma coluna que contenha a representação de sequência da predição. Isso é feito definindo o modeling_role para a coluna como ‘decoded-target’. A documentação para o cliente python do WML está disponível em: http://wml-api-pyclient-dev.mybluemix.net/#repository. Procure “OUTPUT_DATA_SCHEMA” para entender o esquema de saída e a API a ser usada é a API store_model que aceita o OUTPUT_DATA_SCHEMA como um parâmetro.



