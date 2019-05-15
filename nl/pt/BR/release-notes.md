---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: release notes, what's new 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# O quê há de novo
{: #rn-relnotes}

Este documento descreve novos recursos e problemas conhecidos para o {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 5 de Março de 2019
{: #rn-5March2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

### Novos Recursos e Mudanças
{: #rn-5March2019nf}

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação anterior incluem:

- __*Novo modelo Risco de crédito*__: um novo exemplo/tutorial do modelo Risco de crédito é suportado para todos os mecanismos de pontuação. Para obter mais informações, consulte os tópicos [Introdução](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) e [Recursos adicionais](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Despropensão de cálculo*__: é possível alternar entre o seu modelo de produção e um modelo despropenso criado pelo {{site.data.keyword.aios_short}}. Consulte [Modelo de produção e modelo despropenso](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) e [Entendendo como a despropensão funciona](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) para obter mais informações.

## 22 de fevereiro de 2019
{: #rn-22February2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

### Novos Recursos e Mudanças
{: #rn-22February2019nf}

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação anterior incluem:

- __*Atualizações de IU*__: é possível importar um arquivo JSON para configurar programaticamente todos os monitores e recursos durante a criação da assinatura. Também é possível exportar o arquivo de configuração. Consulte o tópico [Configurar assinatura de implementação usando arquivos JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) para obter mais informações.

## 7 de Fevereiro de 2019
{: #rn-7February2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

### Novos Recursos e Mudanças
{: #rn-7February2019nf}

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação anterior incluem:

- __*Atualizações de IU*__: várias melhorias foram feitas na interface com o usuário do {{site.data.keyword.aios_short}}, incluindo uma maneira de [verificar a justiça e a precisão on demand](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep) e a capacidade de ver uma lista de transações por meio do [gráfico de detalhes de justiça](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Aprimoramentos de explicabilidade*__: todos os números têm agora a mesma precisão/escala em valores Pertinent Positive (PP) e Pertinent Negative (PN).

- __*Suporte a SSL do Db2*__: o {{site.data.keyword.aios_short}} suporta a aprovação de certificados autoassinados (codificados em Base-64) com credenciais do DB2.

- __*Suporte ao IBM Cloud Database*__: o {{site.data.keyword.aios_short}} suporta agora o Databases for PostgreSQL, além do Compose for PostgreSQL e Db2)

### Problemas Conhecidos
{: #rn-7February2019ki}

- **Instância de serviço ML customizada**

    - O [módulo Python](/docs/services/ai-openscale?topic=ai-openscale-as-module) não tem atualmente a Explicabilidade funcionando para a instância de serviço Customizado. Isso é porque a instância de serviço Customizado requer uma predição numérica nos dados de resposta, que não está incluída com o script de módulo.

## 14 de dezembro de 2018
{: #rn-14December2018}

Os novos recursos, mudanças e problemas conhecidos a seguir com o serviço estão disponíveis.

### Novos Recursos e Mudanças
{: #rn-12nf}

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação beta incluem:

- __*Disponibilidade geral*__: a liberação de Disponibilidade Geral (GA) do {{site.data.keyword.aios_full_notm}} como um plano IBM Cloud Standard (pago).

- __*IBM Cloud Private for Data V1.2*__: se você estiver usando o {{site.data.keyword.aios_short}} no IBM Cloud Private for Data V1.2, consulte a documentação, incluindo as instruções de instalação, aqui: [Lista de verificação da instalação](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Suporte para seu tipo de modelo*__: além das implementações de modelo IA no Watson Machine Learning, o {{site.data.keyword.aios_short}} suporta implementações de modelo no Microsoft Azure, Amazon SageMaker e em ambientes Customizados. Consulte [Tipos de modelo suportados](/docs/services/ai-openscale?topic=ai-openscale-in-ov) para obter mais informações.

- __*Banco de dados "lite" grátis*__: um banco de dados gerenciado "lite" grátis fornece tudo o que você precisa para começar a usar o {{site.data.keyword.aios_short}}. Consulte os [Planos de precificação do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/watson-openscale){: new_window} para obter detalhes.

- __*Monitoramento de propensão*__: suporte para os atributos protegidos do tipo `float` e `double` e a detecção de propensão em modelos de regressão linear. Além disso, o {{site.data.keyword.aios_short}} pode fazer automaticamente a despropensão de seu modelo IA. Consulte [Entendendo a justiça](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) para obter mais informações.

- __*Explicabilidade*__: suporte para modelos de regressão, funções Python e explicações contrastantes complementares. Consulte [Monitorando explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) para obter mais informações.

- __*Armazenamento de dados*__: o monitoramento de qualidade sem reliance no Watson Machine Learning e a capacidade de usar seu próprio banco de dados, seja Db2, Postgres ou Db2 on Cloud.

- __*NeuNetS (beta)*__: o IBM Neural Network Synthesizer (NeuNetS) está disponível como uma liberação beta (somente nuvem pública). Consulte a [documentação do NeuNetS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window} para obter mais informações.

- __*IU aprimorada*__: a IU do {{site.data.keyword.aios_short}} foi melhorada para incluir uma distribuição de histograma de tempo de execução com alternância para dados de treinamento, ID do modelo e Versão e uma tabela de ID de transação do histograma. Consulte [Visualizando dados para uma hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) para obter mais informações.

- __*Opção de configuração de tutorial alternativo*__: para automatizar o fornecimento e a configuração dos serviços necessários do IBM Cloud e para ver um aplicativo IBM {{site.data.keyword.aios_full}}, incluindo dados de amostra, é possível instalar e executar um módulo Python. Consulte [Instalando um módulo Python para configurar o {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

### Problemas Conhecidos
{: #rn-12ki}

- **Microsoft Azure**

    - Dos dois tipos de serviços da web do Azure Machine Learning, somente o tipo `Novo` é suportado pelo {{site.data.keyword.aios_short}}. O tipo `Classic` não é suportado.

    - __*O nome de entrada padrão deve ser usado*__: no serviço da web Azure, o nome de entrada padrão é `"input1"`. Atualmente, esse campo é obrigatório para o {{site.data.keyword.aios_short}} e, se ele estiver ausente, o {{site.data.keyword.aios_short}} não funcionará.

      Se o seu serviço da web Azure não usar o nome padrão, mude o nome do campo de entrada para `"input1"`, em seguida, o código funcionará.

- **AWS SageMaker**

    - __*O algoritmo BlazingText não é suportado*__: o formato da carga útil de entrada do algoritmo BlazingText do AWS SageMaker não é suportado na liberação atual do {{site.data.keyword.aios_short}}.

## 17 de Setembro de 2018
{: #rn-17September2018}

### Novos Recursos e Mudanças
{: #rn-17nf}

- **Liberação da visualização beta** - bem-vindo à liberação da visualização beta do {{site.data.keyword.aios_full_notm}}.
