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

# Arquitetura 
{: #architecture}

## Replicação

Um serviço {{site.data.keyword.composeForEtcd_full}} contém três membros de dados etcd em um cluster, com seu espaço em disco distribuído pelas zonas de disponibilidade da região e seus dados replicados nos três. Em um cluster etcd, cada membro sabe sobre cada outro membro e conta com um protocolo de consenso distribuído para determinar o líder. O líder transmite seu status de líder em um intervalo configurado. Os seguidores, se nada tiver sido ouvido do líder, terão o seu próprio intervalo, após o qual tentarão se tornar um líder. Quando um membro de dados se torna inacessível, seu cluster continua a operar normalmente.

## Criptografia de Disco

Todos os serviços do  {{site.data.keyword.composeForEtcd}}  têm criptografia em repouso. Seus dados residem em servidores que possuem criptografia em nível de volume ativada. 

Como o {{site.data.keyword.composeForEtcd}} é um serviço gerenciado, é possível que os operadores do {{site.data.keyword.cloud}} Compose vejam dados. Além da criptografia de disco, é necessário criptografar informações pessoais antes de armazená-las no banco de dados ou usar extensões ou recursos para ativar a criptografia no próprio banco de dados. Embora esses métodos possam afetar a usabilidade ou o desempenho, é uma boa prática assegurar-se de que as informações pessoais sejam protegidas com criptografia.

## Auto-scaling

Os recursos são escalados automaticamente com base no uso total de memória dos bancos de dados etcd. O armazenamento baseia-se em uma razão de RAM provisionada em 4:1. Esses recursos são empacotados como unidades.

O Auto-scaling foi projetado para responder às tendências de curto a médio prazo de seu banco de dados. A cada minuto, seu serviço será verificado e, se ele estiver sendo executado com pouca RAM, mais unidades serão alocadas para a implementação. 

O Auto-scaling não reduz a capacidade de implementações em que o uso de disco/memória foi reduzido. Os recursos provisionados para seus bancos de dados são retidos para suas necessidades futuras ou até que você reduza a capacidade de sua implementação manualmente.
{: .tip}
