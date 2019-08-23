---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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

# Perguntas Frequentes
{: #wos-faqs}

Aqui, você encontrará algumas das perguntas mais frequentes de usuários do {{site.data.keyword.aios_full}}.
{: shortdesc}

## Dúvidas
{: #wos-faqs-questions}

- [O que é o {{site.data.keyword.aios_short}}?](#faq-whatsa)
- [Como o {{site.data.keyword.aios_short}} é precificado?](#faq-pricing)
- [Há uma avaliação grátis para o {{site.data.keyword.aios_short}}?](#faq-freetrial)
- [Todos os meus modelos de IA estão no Azure. Posso usar o mecanismo do Microsoft Azure ML com o {{site.data.keyword.aios_short}}?](#faq-azure)
- [Todos os meus modelos de IA estão na Amazon. Posso usar o mecanismo do Amazon SageMaker ML com o {{site.data.keyword.aios_short}}?](#faq-sagemaker)
- [O {{site.data.keyword.aios_short}} está disponível no {{site.data.keyword.icp4dfull_notm}}?](#faq-icp)
- [Desejo executar o {{site.data.keyword.aios_short}} em meus próprios servidores. Quanta energia de processamento do computador devo alocar?](#faq-sizing)
- [Como eu converto uma coluna de predição de um tipo de dados de número inteiro em um tipo de dados categórico?](#wos-faqs-convert-data-types)
- [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos
meus dados de treinamento?](#trainingdata)

### O que é o {{site.data.keyword.aios_short}}?
{: #faq-whatsa}

O Watson OpenScale rastreia e mede os resultados da IA em todo seu ciclo de vida, adaptando e controlando a IA para mudar as situações de negócios para modelos construídos e em execução em qualquer lugar.

Obtenha uma visão geral rápida do {{site.data.keyword.aios_short}} assistindo a este vídeo.

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Confiança e transparência em IA" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

### Como o {{site.data.keyword.aios_short}} é precificado?
{: #faq-pricing}

Quando estiver pronto para a transição do plano Lite, haverá um plano de precificação **Standard** que inclui monitoramento de até 24 modelos implementados, sem restrições sobre o número de carga útil, linhas de feedback ou transações para a explicabilidade. As informações atualizadas estão disponíveis no [catálogo do {{site.data.keyword.Bluemix}}](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external}.


### Há uma avaliação grátis para o {{site.data.keyword.aios_short}}?
{: #faq-freetrial}

O {{site.data.keyword.aios_short}} oferece uma avaliação grátis por meio do plano Lite. Para se inscrever, visite a [página da web do {{site.data.keyword.aios_short}}](https://www.ibm.com/cloud/watson-openscale/){: external} e clique em **Começar agora**. Você poderá usar o plano Lite pelo tempo que desejar (sujeito aos limites de uso mensal que são atualizados a cada mês).

### Todos os meus modelos de IA estão no Azure. Posso usar o mecanismo do Microsoft Azure ML com o {{site.data.keyword.aios_short}}?
{: #faq-azure}

O {{site.data.keyword.aios_short}} suporta os mecanismos do Microsoft Azure ML Studio e do Microsoft Azure ML Service. Para obter mais informações, consulte [Estruturas do Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure) e [Estruturas do serviço Microsoft Azure ML](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service).

### Todos os meus modelos de IA estão na Amazon. Posso usar o mecanismo do Amazon SageMaker ML com o {{site.data.keyword.aios_short}}?
{: #faq-sagemaker}

O {{site.data.keyword.aios_short}} suporta o mecanismo ML do Amazon SageMaker. Para obter mais informações, consulte [Estruturas do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage).

### O {{site.data.keyword.aios_short}} está disponível no {{site.data.keyword.icp4dfull_notm}}?
{: #faq-icp}

O {{site.data.keyword.aios_short}} é um dos complementos premium para o {{site.data.keyword.icp4dfull_notm}}. 

### Desejo executar o {{site.data.keyword.aios_short}} em meus próprios servidores. Quanta energia de processamento do computador devo alocar?
{: #faq-sizing}

Há diretrizes específicas para a [configuração de hardware](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#inst-hwt) para configurações de três nós e de seis nós. A equipe de vendas técnicas da IBM também pode ajudá-lo a dimensionar a sua configuração específica. Como o {{site.data.keyword.aios_short}} é executado como um complemento para o {{site.data.keyword.icp4dfull_notm}}, é necessário considerar os requisitos para ambos os produtos de software.

### Como eu converto uma coluna de predição de um tipo de dados de número inteiro em um tipo de dados categórico?
{: #wos-faqs-convert-data-types}

Ao configurar o monitoramento de justiça para um modelo, a coluna de predição permite somente um valor numérico inteiro mesmo que o rótulo de predição seja categórico. Como configurar isso para o recurso categórico (que não é um número inteiro)? é necessária uma conversão manual? 

Os dados de treinamento podem ter rótulos de classe, como “Loan Denied”, “Loan Granted”. O valor de predição retornado pelo terminal de pontuação do {{site.data.keyword.pm_full}} tem valores como “0.0”, “1.0" etc. O terminal de pontuação também tem uma coluna opcional que contém a representação de texto da predição. Por exemplo, se prediction=1.0, a coluna predictionLabel poderia ter um valor “Loan Granted”. Se essa coluna estiver disponível, enquanto estiver configurando o resultado favorável e desfavorável para o modelo, será possível especificar os valores de sequência “Loan Granted” e “Loan Denied”. Se essa coluna não estiver disponível, será necessário especificar os valores de número inteiro/duplo de 1.0, 0.0 para a classe favorável/desfavorável.

O {{site.data.keyword.pm_full}} tem um conceito de esquema de saída que define o esquema da saída de terminal de pontuação do {{site.data.keyword.pm_full}} e a função para as diferentes colunas. As funções são usadas para identificar qual coluna contém o valor prediction, qual coluna contém a probabilidade de predição e o valor do rótulo de classe etc. O esquema de saída é configurado automaticamente para modelos criados usando o construtor de modelo. Ele também pode ser configurado usando o cliente Python do {{site.data.keyword.pm_full}}. Os usuários podem usar o esquema de saída para definir uma coluna que contenha a representação de sequência da predição. Isso é feito definindo o modeling_role para a coluna como ‘decoded-target’. A documentação para o cliente Python do {{site.data.keyword.pm_full}} está disponível em: http://wml-api-pyclient-dev.mybluemix.net/#repository. Procure “OUTPUT_DATA_SCHEMA” para entender o esquema de saída e a API a ser usada é a API store_model que aceita o OUTPUT_DATA_SCHEMA como um parâmetro.

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


