---

copyright:
  years: 2017
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 备份
{: #backups}

您可以从服务仪表板*管理*页面的_备份_选项卡创建和下载备份。可以使用安排的备份和手动备份。可以使用安排的备份和手动备份。

## 查看现有备份

数据库的每日备份会自动安排。要查看现有备份：

1. 浏览至服务仪表板的_管理_页面。
2. 单击选项卡中的**备份**以打开_备份_页面。此时将显示可用备份列表：

  ![可用备份](./images/etcd-backups-show.png "可用备份列表")

单击相应的行以展开任何可用备份的选项。
  ![备份选项](./images/etcd-backups-options.png "备份选项。") 

## 创建手动备份

除了已安排的备份，您还可以手动创建备份。要创建手动备份，请执行以下步骤以查看现有备份，然后单击可用备份列表上方的**现在备份**。此时将显示一条消息，通知您已启动备份，并且“暂挂”备份将添加到可用备份列表中。

## 下载备份

要下载备份，请执行以下步骤以查看现有备份，然后单击相应的行以展开要下载的备份的选项。单击**下载**按钮。该压缩文件包含用于本地使用的数据的二进制快照。

## 复原备份
要将备份复原到新服务实例，请执行以下步骤以查看现有备份，然后单击相应的行以展开要下载的备份的选项。单击**复原**按钮。此时将显示一条消息，通知您已启动复原。新服务实例将自动命名为“etcd-restore-[timestamp]”，并在供应启动时显示在仪表板上。