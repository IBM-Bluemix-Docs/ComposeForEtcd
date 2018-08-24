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

# Architektur 
{: #architecture}

## Replikation

Ein {{site.data.keyword.composeForEtcd_full}}-Service enthält drei etcd-Datenelemente (Member) in einem Cluster, deren Plattenspeicher über die Verfügbarkeitszonen der Region verteilt ist. Ihre Daten werden auf allen drei Datenelementen (Membern) repliziert. In einem etcd-Cluster ist jedes Member über jedes andere Member informiert und stützt sich zur Bestimmung des 'Leaders' auf ein Protokoll des verteilten Konsens. Der Leader sendet seinen Leaderstatus in festgelegten Intervallen rund. Für den Fall, dass es keinerlei Neuigkeiten vom 'Leader' gibt, gilt für jeden 'Follower' ein eigenes Intervall, nach dessen Verstreichen versucht wird, selbst 'Leader' zu werden. Sollte ein Datenelement (Member) nicht mehr erreichbar sein, setzt Ihr Cluster seinen Betrieb ordnungsgemäß fort.

## Plattenverschlüsselung

Für alle {{site.data.keyword.composeForEtcd}}-Services erfolgt eine Verschlüsselung im Ruhezustand. Ihre Daten befinden sich auf Servern, auf denen die Verschlüsselung auf Datenträgerebene aktiviert ist. 

Da es sich bei {{site.data.keyword.composeForEtcd}} um einen verwalteten Service handelt, sind Operatoren von Compose auf {{site.data.keyword.cloud}} in der Lage, Daten zu sehen. Zusätzlich zur Plattenverschlüsselung sollten Sie persönliche Informationen verschlüsseln, bevor diese in der Datenbank gespeichert werden, oder Sie sollten Erweiterungen oder Features verwenden, um die Verschlüsselung auf der Datenbank selbst zu ermöglichen. Obwohl diese Methoden den Bedienungskomfort oder die Leistung beeinträchtigen können, hat es sich bewährt, den Schutz persönlicher Informationen mit Verschlüsselung sicherzustellen.

## Automatische Skalierung

Die Ressourcen werden basierend auf der Gesamtspeicherbelegung der etcd-Datenbanken automatisch skaliert. Der Speicher basiert auf einem Faktor des bereitgestellten Arbeitsspeichers im Verhältnis von 4:1. Diese Ressourcen werden als Einheiten gebündelt.

Die automatische Skalierung ist so konzipiert, dass sie als Reaktion auf die kurz-bis mittelfristigen Trends Ihrer Datenbank erfolgt. Ihr Service wird in Minutenintervallen überprüft. Wenn der Arbeitsspeicher für den Service knapp zu werden droht, werden der Bereitstellung weitere Einheiten zugeordnet. 

Bei der automatischen Skalierung wird kein Scale-down für Bereitstellungen durchgeführt, bei denen sich die Platten-/Speicherbelegung verringert hat. Die für Ihre Datenbanken bereitgestellten Ressourcen bleiben für künftige Anforderungen weiterhin bestehen, sofern Sie Ihre Bereitstellung nicht per Scale-down manuell nach unten skalieren.
{: .tip}
