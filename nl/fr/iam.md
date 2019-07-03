---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## Rôles et actions d'Identity and Access Management

L'accès aux instances de service {{site.data.keyword.aios_full}} pour les utilisateurs de votre compte
est contrôlé par {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM).
A chaque utilisateur qui accède au service {{site.data.keyword.aios_short}} dans votre compte doit être attribué une règle d'accès avec un rôle IAM défini.
La règle détermine les actions qu'un utilisateur peut effectuer dans le contexte du service ou de l'instance sélectionnée.
Les actions autorisées sont personnalisées et définies par le service {{site.data.keyword.Bluemix_notm}} en tant qu'opérations pouvant être réalisées sur le service.
Les actions sont ensuite mappées aux rôles utilisateur IAM.

Les règles permettent d'accorder l'accès à différents niveaux.
Voici quelques-unes des options : 

* Accès à toutes les instances du service de votre compte
* Accès à une instance de service particulière de votre compte
* Accès à une ressource spécifique dans une instance

Une fois que vous avez défini l'étendue de la règle d'accès, vous attribuez un rôle qui détermine le niveau d'accès de l'utilisateur.
Consultez les tableaux suivants qui décrivent les actions que chaque rôle autorise dans le service {{site.data.keyword.aios_short}}.

Le tableau suivant détaille les actions mappées sur les rôles de gestion de plateforme.
Les rôles de gestion de plateforme permettent aux utilisateurs d'effectuer des tâches sur les ressources de service au niveau de la plateforme, par exemple, attribuer un accès utilisateur au service, créer ou supprimer des instances et lier des instances aux applications.

| Rôle de gestion plateforme | Description des actions | Exemples d'action                                               |
|--------------------------|------------------------|-----------------------------------------------------------------|
| Visualiseur                | Description             | <ul><li>Exemple 1</li><li>Exemple 2</li></ul>                   |
| Editeur                    | Description             |<ul><li>Exemple 1</li><li>Exemple 2</li></ul>                    |
| Opérateur                  | Description             | <ul><li>Exemple 1</li><li>Exemple 2</li><li>Exemple 3</li></ul> |
| Administrateur             | Description             |<ul><li>Exemple 1</li><li>Exemple 2</li><li>Exemple 3</li></ul>  |
{: caption="Tableau 1. Rôles d'utilisateur et actions IAM" caption-side="top"}


Le tableau suivant détaille les actions qui sont mappées aux rôles d'accès aux services.
Les rôles d'accès aux services permettent aux utilisateurs d'accéder à {{site.data.keyword.aios_short}} ainsi que la possibilité d'appeler l'API {{site.data.keyword.aios_short}}.

| Rôle d'accès au service | Description des actions | Exemples d'action                                               |
|---------------------|------------------------|-----------------------------------------------------------------|
| Lecteur                 | Description             | <ul><li>Exemple 1</li><li>Exemple 2</li></ul>                   |
| Auteur                  | Description             |<ul><li>Exemple 1</li><li>Exemple 2</li></ul>                    |
| Gestionnaire            | Description             | <ul><li>Exemple 1</li><li>Exemple 2</li><li>Exemple 3</li></ul> |
{: caption="Tableau 2. Rôles d'accès au service et actions IAM" caption-side="top"}


Pour plus d'informations sur l'attribution de rôles d'utilisateur dans l'interface utilisateur, voir [Gestion de l'accès aux ressources](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
