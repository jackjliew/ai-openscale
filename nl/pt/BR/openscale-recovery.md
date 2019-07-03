---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# Alta disponibilidade e recuperação de desastre
{: #openscale-availability-recovery}

O {{site.data.keyword.aios_full}} está altamente disponível dentro de múltiplos locais do {{site.data.keyword.cloud_notm}}, como Dallas e Washington, DC. No entanto, a recuperação de potenciais desastres que afetam um local inteiro requer planejamento e preparação.
{: shortdesc}

Você é responsável por entender sua configuração, customização e uso do serviço. Você também é responsável por estar pronto para recriar uma instância do serviço em um novo local e para restaurar seus dados em qualquer local. Consulte [Como assegurar tempo de inatividade zero?](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external} para obter informações adicionais.

## Alta disponibilidade 
{: #openscale-high-availability}

O {{site.data.keyword.aios_short}} é implementado e está disponível nos data centers **us-south** com multiple zone routing (MZR) em três zonas de disponibilidade. A qualquer momento, se uma zona não estiver disponível, o sistema continuará a estar disponível em outras zonas de disponibilidade. O balanceador de carga global e o servidor DNS roteiam o tráfego para as zonas disponíveis sem qualquer interrupção do usuário.

Os dados que são armazenados em bancos de dados PostgreSQL também estão altamente disponíveis e existem em múltiplas zonas de disponibilidade. No entanto, a responsabilidade do cliente é fazer backup de dados no suporte de um plano de recuperação de desastres para que os serviços possam ser recriados.

O tráfego do {{site.data.keyword.aios_short}} tem a carga balanceada em múltiplas zonas em uma região. Cada zona é um data center na mesma região. 

Os bancos de dados do Compose, como o PostgreSQL, e os bancos de dados do diretório <code>etc</code> distribuído (etcd) são submetidos a backup periodicamente para assegurar a alta disponibilidade e, no caso de desastre, a equipe de operações do {{site.data.keyword.aios_short}} poderá recuperar o serviço no Objetivo do Ponto de Recuperação (RPO).
 
O {{site.data.keyword.cloud_notm}} oferece redundância de dados na região que permite proteção de alta disponibilidade. A IBM fornece replicação automática de dados para bancos de dados do cliente que contêm treinamento e/ou dados de modelo customizado sem custo adicional. A replicação é concluída em zonas de disponibilidade na região dentro de data centers do {{site.data.keyword.cloud_notm}}.
 
## Fazer backup e restauração
{: #openscale-restore}

Os clientes são responsáveis por fazer backup e restaurar seus próprios dados, incluindo treinamento e/ou dados de modelo customizado, assim como quaisquer modelos customizados gerados pelo Cliente. Para obter instruções de backup e restauração do cliente, consulte a documentação do {{site.data.keyword.cloud_notm}}.
 
## Recuperação de desastre
{: #openscale-disaster-recovery}

A Continuidade de Negócios na região é concluída alavancando a replicação automática entre as zonas de disponibilidade na região dentro dos data centers do {{site.data.keyword.cloud_notm}}. Os clientes são responsáveis pela Recuperação de desastre multirregião. As responsabilidades incluem o backup, a restauração e a sincronização de suas próprias políticas de segurança, treinamento e/ou dados de modelo customizado, assim como quaisquer modelos customizados gerados pelo cliente. Além disso, o cliente é responsável pelo roteamento e/ou balanceamento de carga entre as regiões. Para obter instruções de backup e restauração do cliente, consulte a documentação do {{site.data.keyword.cloud_notm}}.
