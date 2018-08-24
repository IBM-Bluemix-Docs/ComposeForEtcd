---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Architettura 
{: #architecture}

## Replica

Un servizio {{site.data.keyword.composeForEtcd_full}} contiene tre membri di dati etcd in un cluster, con il loro spazio su disco distribuito sulle zone di disponibilità della regione e i tuoi dati replicati tra tutti e tre. In un cluster etcd, ciascun membro è a conoscenza di ogni altro membro e si basa su un protocollo di consenso distribuito per determinare il leader. Il leader trasmette il suo stato di leader a un intervallo impostato. I follower, in assenza di comunicazioni dal leader, hanno tutti un loro intervallo dopo il quale provano a diventare leader. Se un membro di dati diventa irraggiungibile, il tuo cluster continua a funzionare normalmente.

## Crittografia del disco

Tutti i servizi {{site.data.keyword.composeForEtcd}} hanno la crittografia dei dati inattivi. I tuoi dati si trovano su server che hanno la crittografia a livello di volume abilitata. 

Poiché {{site.data.keyword.composeForEtcd}} è un servizio gestito, gli operatori di {{site.data.keyword.cloud}} Compose possono visualizzare i dati. Oltre alla crittografia del disco, devi crittografare le informazioni personali prima di archiviarle nel database o usare delle estensioni o delle funzioni per abilitare la crittografia sul database stesso. Anche se questi metodi possono influire sull'usabilità o sulle prestazioni, è buona norma assicurarsi che le informazioni personali siano protette con la crittografia.

## Ridimensionamento automatico

Le risorse vengono ridimensionate automaticamente in base all'utilizzo della memoria totale dei database etcd. L'archiviazione è basata su un rapporto di RAM di cui viene eseguito il provisioning di 4:1. Queste risorse sono raccolte in bundle come unità.

Il ridimensionamento automatico è progettato per rispondere alle tendenze a medio e a lungo termine del tuo database. Il tuo servizio viene controllato ogni minuto e, se sta esaurendo la RAM, delle ulteriori unità vengono assegnate alla distribuzione. 

Il ridimensionamento automatico non riduce le distribuzioni in cui l'utilizzo di disco/memoria si è ridotto. Le risorse di cui è stato eseguito il provisioning ai tuoi database vengono conservate per le tue future esigenze oppure finché non riduci manualmente la tua distribuzione.
{: .tip}
