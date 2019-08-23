---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


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
est contrôlé par {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). A chaque utilisateur qui accède au service {{site.data.keyword.aios_short}} dans votre compte doit être attribué une politique d'accès avec un rôle IAM défini. La politique détermine les actions qu'un utilisateur peut effectuer dans le contexte du service ou de l'instance sélectionnée. Les actions autorisées sont personnalisées et définies par le service {{site.data.keyword.Bluemix_notm}} en tant qu'opérations pouvant être réalisées sur le service. Les actions sont ensuite mappées aux rôles utilisateur IAM.

Les politiques permettent d'accorder l'accès à différents niveaux. Voici quelques-unes des options : 

* Accès à toutes les instances du service de votre compte
* Accès à une instance de service particulière de votre compte
* Accès à une ressource spécifique dans une instance

Une fois que vous avez défini l'étendue de la politique d'accès, vous attribuez un rôle qui détermine le niveau d'accès de l'utilisateur. Consultez les tableaux suivants qui décrivent les actions que chaque rôle autorise dans le service {{site.data.keyword.aios_short}}.

Les rôles de gestion de plateforme permettent d'attribuer aux utilisateurs des degrés d'autorisation différents pour effectuer des actions de plateforme dans le compte et sur un service. Par exemple, les rôles de gestion de plateforme affectés pour les ressources de catalogue permettent aux utilisateurs d'effectuer des actions comme la création, la suppression, l'édition et l'affichage d'instances de service. Les services de gestion de plateforme affectés pour les services de gestion de service permettent aux utilisateurs d'effectuer des actions comme l'invitation et la suppression d'utilisateurs, l'utilisation de groupes de ressources et l'affichage des informations de facturation. Pour plus d'informations sur les services de gestion de compte, consultez [Affectation de l'accès aux services de gestion de compte](/docs/iam?topic=iam-account-services#account-services){: external}.

Lors de la création d'une politique, sélectionnez tous les rôles applicables. Chaque rôle permet d'effectuer des actions séparées et n'hérite pas des actions des rôles inférieurs.
{: tip}

Le tableau suivant fournit des exemples de certaines actions de gestion de plateforme que les utilisateurs peuvent effectuer dans le contexte de ressources de catalogue et de groupes de ressources. Pour comprendre comment les rôles s'appliquent aux utilisateurs dans le contexte du service que vous utilisez, reportez-vous à la documentation de chaque offre de catalogue.


|  | Un ou tous les services activés pour IAM | Service sélectionné dans un groupe de ressources | Groupe de ressources sélectionné |
|:--------------|:------------|:-------------|:-------------|
| Rôle Afficheur | Afficher des instances, des alias, des liaisons et des données d'identification | Afficher uniquement des instances spécifiées du groupe de ressources | Afficher un groupe de ressources |
| Rôle Opérateur |  Afficher des instances et gérer des alias, des liaisons et des données d'identification |  Non applicable | Non applicable |
| Rôle Editeur |  Créer, supprimer, éditer et afficher des instances. Gérer des alias, des liaisons et des données d'identification | Créer, supprimer, éditer, suspendre, reprendre, afficher et lier uniquement des instances spécifiées du groupe de ressources | Afficher et éditer le nom d'un groupe de ressources |
| Rôle Administrateur |  Toutes les actions de gestion pour les services | Toutes les actions de gestion pour des instances spécifiées du groupe de ressources | Afficher, éditer et gérer l'accès pour le groupe de ressources |
| Rôle Administrateur du cluster (spécifique à {{site.data.keyword.wos4d_full}}) |  Bénéficie d'un accès total à la plateforme IBM Cloud Private | Bénéficie d'un accès total aux instances spécifiées du groupe de ressources | Les actions suivantes ne peuvent être effectuées que par l'administrateur du cluster : se
connecter à un annuaire LDAP, ajouter des utilisateurs et leur attribuer les rôles IAM,
gérer les charges de travail, l'infrastructure et les applications dans tous les espaces
de noms, créer des espaces de noms, affecter des quotas, ajouter des politiques de
sécurité de pod, ajouter un référentiel Helm interne, supprimer un référentiel Helm
interne, ajouter des graphiques Helm au référentiel Helm interne, supprimer des
graphiques Helm du référentiel Helm interne et synchroniser les référentiels Helm
internes et externes. |
{: row-headers}
{: class="comparison-table"}
{: caption="Tableau 1. Exemple de rôles et d'actions de gestion de plateforme pour les services d'un compte" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


Pour les rôles d'accès au service, qui permettent aux utilisateurs d'accéder à {{site.data.keyword.aios_short}} et leur donnent également la possibilité d'appeler l'API REST, {{site.data.keyword.aios_short}} s'en remet aux rôles de gestion de plateforme listés dans le tableau précédent. Pour plus d'informations sur l'attribution de rôles d'utilisateur dans l'interface utilisateur, consultez [Gestion de l'accès aux ressources](/docs/iam?topic=iam-iammanidaccser#iammanidaccser){: external}.

 
