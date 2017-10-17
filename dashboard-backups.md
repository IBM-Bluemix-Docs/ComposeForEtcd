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

# Backups
{: #backups}

You can create and download backups from the _Backups_ tab of the *Manage* page of your service dashboard. Both scheduled and manual backups are available. Both scheduled and manual backups are available.

## Viewing existing backups

Daily backups of your database are automatically scheduled. To view your existing backups:

1. Navigate to the _Manage_ page of your service Dashboard.
2. Click **Backups** in the tabs to open the _Backups_ page. A list of available backups is shown:

  ![Available backups](./images/etcd-backups-show.png "A list of available backups.")

Click on the corresponding row to expand the options for any available backup.
  ![Backup Options](./images/etcd-backups-options.png "Options for a backup.") 

## Creating a manual backup

As well as scheduled backups you can create a backup manually. To create a manual backup, follow the steps to view existing backups, then click **Back up now** above the list of available backups. A message is displayed to let you know that a backup has been initiated, and a 'pending' backup is added to the list of available backups.

## Downloading a backup

To download a backup, follow the steps to view existing backups, then click in the corresponding row to expand the options for the backup you want to download. Click on the **Download** button. The compressed file contains a binary snapshot of your data for use locally.

## Restoring a backup
To restore a backup to a new service instance, follow the steps to view existing backups, then click in the corresponding row to expand the options for the backup you want to download. Click on the **Restore** button. A message is displayed to let you know that a resotre has been initiated. The new service instance will automatically be named "etcd-restore-[timestamp]", and appears on your dashboard when provisioning starts.