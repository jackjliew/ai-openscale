---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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
{:faq: data-hd-content-type='faq'}

# Perguntas Frequentes
{: #wos-faqs}

Aqui, você encontrará algumas das perguntas mais frequentes de usuários do {{site.data.keyword.aios_full}}.
{: shortdesc}

## Dúvidas
{: #wos-faqs-questions}

- [Como eu converto uma coluna de predição de um tipo de dados de número inteiro em um tipo de dados categórico?](#wos-faqs-convert-data-types)
- [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos
meus dados de treinamento?](#trainingdata)

### Como eu converto uma coluna de predição de um tipo de dados de número inteiro em um tipo de dados categórico?
{: #wos-faqs-convert-data-types}

Ao configurar o monitoramento de justiça para um modelo, a coluna de predição permite somente um valor numérico inteiro mesmo que o rótulo de predição seja categórico. Como configurar isso para o recurso categórico (que não é um número inteiro)? é necessária uma conversão manual? 

Os dados de treinamento podem ter rótulos de classe, como “Loan Denied”, “Loan Granted”. O valor prediction retornado pelo terminal de pontuação do WML tem valores como “0.0”, “1.0" etc. O terminal de pontuação também tem uma coluna opcional que contém a representação de texto da predição. Por exemplo, se prediction=1.0, a coluna predictionLabel poderia ter um valor “Loan Granted”. Se essa coluna estiver disponível, enquanto estiver configurando o resultado favorável e desfavorável para o modelo, será possível especificar os valores de sequência “Loan Granted” e “Loan Denied”. Se essa coluna não estiver disponível, será necessário especificar os valores de número inteiro/duplo de 1.0, 0.0 para a classe favorável/desfavorável.

O WML tem um conceito de esquema de saída que define o esquema da saída do terminal de pontuação do WML e a função para as colunas diferentes. As funções são usadas para identificar qual coluna contém o valor prediction, qual coluna contém a probabilidade de predição e o valor do rótulo de classe etc. O esquema de saída é configurado automaticamente para modelos criados usando o construtor de modelo. Isso também pode ser configurado usando o cliente python do WML. Os usuários podem usar o esquema de saída para definir uma coluna que contenha a representação de sequência da predição. Isso é feito definindo o modeling_role para a coluna como ‘decoded-target’. A documentação para o cliente python do WML está disponível em: http://wml-api-pyclient-dev.mybluemix.net/#repository. Procure “OUTPUT_DATA_SCHEMA” para entender o esquema de saída e a API a ser usada é a API store_model que aceita o OUTPUT_DATA_SCHEMA como um parâmetro.

### Por que o {{site.data.keyword.aios_short}} precisa de acesso aos meus dados de treinamento?
{: #trainingdata}

Deve-se fornecer ao {{site.data.keyword.aios_short}} o acesso aos dados de treinamento
que estão armazenados no Db2 ou no {{site.data.keyword.cos_full_notm}} ou deve-se executar um bloco de notas que possa acessar os dados de treinamento. O {{site.data.keyword.aios_short}} precisa de acesso
aos dados de treinamento pelos motivos a seguir:

- Para gerar explicações contrastantes: para criar explicações, é necessário o acesso a
estatísticas dos dados de treinamento, como valor mediano, desvio padrão e valores distintos.
- Para exibir estatísticas de dados de treinamento: para preencher a página de detalhes de propensão,
o {{site.data.keyword.aios_short}} deve ter dados de treinamento dos quais gerar estatísticas.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

Na abordagem baseada em bloco de notas, espera-se que você faça upload de estatísticas e outras informações ao configurar uma implantação no {{site.data.keyword.aios_short}}. Isso implica que
o {{site.data.keyword.aios_short}} não tem mais acesso aos dados de treinamento fora do bloco de
notas, o qual é executado em seu ambiente. Ele tem acesso somente às informações transferidas por upload
durante a configuração.


