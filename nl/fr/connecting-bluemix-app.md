---

copyright:
  years: 2016,2017
lastupdated: "2017-09-21"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connexion d'une application {{site.data.keyword.cloud_notm}}

Pour connecter une application {{site.data.keyword.cloud}} à votre service, utilisez les données d'identification créées lors de la mise à disposition du service. Le modèle d'application montre comment utiliser Node.js pour établir une connexion à un service {{site.data.keyword.composeForEtcd}} à l'aide des données d'identification fournies et comment créer une base de données, lire dans cette base de données et y écrire.

## Connexion à l'aide du modèle d'application 'Hello World'

Le modèle d'application [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) montre comment utiliser Node.js pour établir une connexion à un service {{site.data.keyword.composeForEtcd}} à l'aide des données d'identification fournies. L'application crée une base de données, y lit et y écrit.

Téléchargez le modèle d'application et suivez les instructions contenues dans le fichier Readme. Ensuite, sur la page des détails d'application d'{{site.data.keyword.cloud}}, cliquez sur **Afficher l'application** pour afficher le contenu du tableau *Exemples*.

## Données d'identification disponibles
{: #available-credentials}

Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service. Le modèle d'application [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) montre comment utiliser Node.js pour établir une connexion à un service {{site.data.keyword.composeForEtcd}} à l'aide des données d'identification.

|Nom de zone|Description|
|----------|-----------|
|`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte au serveur approprié. Le certificat est codé en base64. Vous devez décoder la clé avant de l'utiliser, comme illustré dans le modèle d'application.|
|`deployment_id`|Identificateur interne du service, créé dans Compose.|
|`db_type`|Type de base de données fourni par le service, en l'occurrence, `etcd`.|
|`name`|Nom du déploiement de base de données.|
|`uri`|URI à utiliser pour établir la connexion au service. `uri`
comprend le schéma (`amqps:), le nom et le mot de passe de l'administrateur, le
nom d'hôte du serveur et le numéro de port auquel se connecter, ainsi que le nom `vhost`.|
{: caption="Tableau 1. Données d'identification Compose for etcd" caption-side="top"}
