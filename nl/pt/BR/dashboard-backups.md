---

Copyright:
  Years: 2017
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Backups
{: #backups}

É possível criar e fazer download de backups na guia _Backups_ da página *Gerenciar* de seu painel de serviço. Ambos os backups, planejado e manual, estão disponíveis. Ambos os backups, planejado e manual, estão disponíveis.

## Visualizando backups existentes

Os backups diários de seu banco de dados são planejados automaticamente. Para visualizar seus backups existentes:

1. Navegue para a página _Gerenciar_ de seu Painel de serviço.
2. Clique em **Backups** nas guias para abrir a página _Backups_. Uma lista de backups disponíveis é mostrada:

  ![Available backups](./images/etcd-backups-show.png "A list of available backups.")

Clique na linha correspondente para expandir as opções para qualquer backup disponível.
  ![Backup Options](./images/etcd-backups-options.png "Options for a backup.") 

## Criando um backup manual

Além de backups planejados, é possível criar um backup manualmente. Para criar um backup manual, siga as etapas para visualizar os backups existentes, em seguida, clique em **Fazer backup agora** acima da lista de backups disponíveis. Uma mensagem é exibida para permitir que você saiba que um backup foi iniciado e um backup 'pendente' é incluído na lista de backups disponíveis.

## Fazendo download de um backup

Para fazer download de um backup, siga as etapas para visualizar os backups existentes, em seguida, clique na linha correspondente para expandir as opções para o backup que você deseja fazer download. Clique no botão **Download**. O arquivo compactado contém uma captura instantânea binária de seus dados para ser usada localmente.

## Restaurando um backup
Para restaurar um backup para uma nova instância de serviço, siga as etapas para visualizar os backups existentes, em seguida, clique na linha correspondente para expandir as opções para o backup que você deseja fazer download. Clique no botão **Restaurar**. Uma mensagem é exibida para permitir que você saiba que uma restauração foi iniciada. A nova instância de serviço será nomeada automaticamente "etcd-restore-[timestamp]" e aparecerá em seu painel quando o fornecimento iniciar.
