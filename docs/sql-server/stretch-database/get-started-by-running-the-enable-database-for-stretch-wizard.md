---
title: "Get started by running the Enable Database for Stretch Wizard"
description: "Get started by running the Enable Database for Stretch Wizard"
ms.date: "08/05/2016"
ms.service: sql-server-stretch-database
ms.reviewer: ""
ms.topic: quickstart
f1_keywords: 
  - "sql13.swb.stretchwizard.f1"
  - "sql13.swb.stretchwizard.createdatabasecredentials.f1"
  - "sql13.swb.stretchwizard.selectdatabasetables.f1"
  - "sql13.swb.stretchwizard.validatesqlserver.f1"
  - "sql13.swb.stretchwizard.selectazuredeployment.f1"
  - "sql13.swb.stretchwizard.configureazuredeployment.f1"
  - "sql13.swb.stretchwizard.Summary.f1"
  - "sql13.swb.stretchwizard.Results.f1"
  - "sql13.swb.stretchwizard.introduction.f1"
helpviewer_keywords:
  - "Stretch Database, wizard"
  - "Enable Database for Stretch Wizard"
ms.assetid: 855dd9fc-f80c-4dbc-bf46-55a9736bfe15
author: MikeRayMSFT
ms.author: mikeray
ms.custom:
  - seo-dt-2019
  - intro-quickstart
---
# Get started by running the Enable Database for Stretch Wizard
[!INCLUDE [sqlserver2016-windows-only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]


 To configure a database for Stretch Database, run the Enable Database for Stretch Wizard.  This article describes the info that you have to enter and the choices that you have to make in the wizard.  
  
 To learn more about Stretch Database, see [Stretch Database](../../sql-server/stretch-database/stretch-database.md). 
 
 > [!NOTE] 
 > Later, if you disable Stretch Database, remember that disabling Stretch Database for a table or for a database does not delete the remote object. If you want to delete the remote table or the remote database, you have to drop it by using the Azure management portal. The remote objects continue to incur Azure costs until you delete them manually. 
  
## Launch the wizard  
  
1.  In SQL Server Management Studio, in Object Explorer, select the database on which you want to enable Stretch.  
  
2.  Right-click and select **Tasks**, and then select **Stretch**, and then select **Enable** to launch the wizard.  
  
##  <a name="Intro"></a> Introduction  
 Review the purpose of the wizard and the prerequisites.  
 
 The important prerequisites include the following.
 -   You have to be an administrator to change database settings.
 -   You have to have a Microsoft Azure subscription.
 -   Your SQL Server has to be able to communicate with the remote Azure server.
  
 ![Introduction page of Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-1.png "Introduction page of Stretch Database wizard")  
  
##  <a name="Tables"></a> Select tables  
 Select the tables that you want to enable for Stretch.  
 
Tables with lots of rows appear at the top of the sorted list. Before the Wizard displays the list of tables, it analyzes them for data types that are not currently supported by Stretch Database. 
  
 ![Select tables page of Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-2.png "Select tables page of Stretch Database wizard")  
  
|Column|Description|  
|------------|-----------------|  
|(no title)|Check the check box in this column to enable the selected table for Stretch.|  
|**Name**|Specifies the name of the table in the database.|  
|(no title)|A symbol in this column may represent a warning that doesn't prevent you from enabling the selected table for Stretch. It may also represent a blocking issue that prevents you from enabling the selected table for Stretch - for example, because the table uses an unsupported data type. Hover over the symbol to display more info in a tooltip. For more info, see [Limitations for Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).|  
|**Stretched**|Indicates whether the table is already enabled for Stretch.|  
|**Migrate**|You can migrate an entire table (**Entire Table**) or you can specify a filter on an existing column in the table. If you want to use a different filter function to select rows to migrate, run the ALTER TABLE statement to specify the filter function after you exit the wizard. For more info about the filter function, see [Select rows to migrate by using a filter function](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). For more info about how to apply the function, see [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) or [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).|  
|**Rows**|Specifies the number of rows in the table.|  
|**Size (KB)**|Specifies the size of the table in KB.|  
  
## Optionally provide a row filter  
 If you want to provide a filter function to select rows to migrate, do the following things on the **Select tables** page.  
  
1.  In the **Select the tables you want to stretch** list, click **Entire Table** in the row for the table. The **Select rows to stretch** dialog box opens.  
  
     ![Define a date-based filter predicate](../../sql-server/stretch-database/media/stretch-wizard-2a.png "Define a date-based filter predicate")  
  
2.  In the **Select rows to stretch** dialog box, select **Choose Rows**.  
  
3.  In the **Name field**, provide a name for the filter function.  
  
4.  For the **Where** clause, pick a column from the table, pick an operator, and provide a value.  
  
5.  Click **Check** to test the function. If the function returns results from the table - that is, if there are rows to migrate that satisfy the condition - the test reports **Success**.  

> [!NOTE] 
> The textbox that displays the filter query is read-only. You can't edit the query in the textbox.
  
6.  Click Done to return to the **Select tables** page.  

The filter function is created in SQL Server only when you finish the wizard. Until then, you can return to the **Select tables** page to change or rename the filter function.

![Select Tables page after defining a filter predicate](../../sql-server/stretch-database/media/stretch-wizard-2b.png "Select Tables page after defining a filter predicate")

If you want to use a different type of filter function to select rows to migrate, do one of the following things.  
  
-   Exit the wizard and run the ALTER TABLE statement to enable Stretch for the table and to specify a filter function. For more info, see [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
-   Run the ALTER TABLE statement to specify a filter function after you exit the wizard. For the required steps, see [Add a filter function after running the Wizard](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
##  <a name="Configure"></a> Configure Azure  
  
1.  Sign in to Microsoft Azure with a Microsoft account.  
  
     ![Sign in to Azure - Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-3.png "Sign in to Azure - Stretch Database wizard")  
  
2.  Select the existing Azure subscription to use for Stretch Database. 

> [!NOTE] 
> To enable Stretch on a database you must have administrator rights to the subscription you are using. Stretch Database wizard will only show subscriptions where the user has administrator rights.
  
3.  Select the Azure region to use for Stretch Database.
    -   If you create a new server, the server is created in this region.  
    -   If you have existing servers in the selected region, the wizard lists them when you choose **Existing server**.
  
     To minimize latency, pick the Azure region in which your SQL Server is located. For more info about regions, see [Azure Regions](https://azure.microsoft.com/regions/).  
  
4.  Specify whether you want to use an existing server or create a new Azure server.  
  
     If the Active Directory on your SQL Server is federated with Azure Active Directory, you can optionally use a federated service account for SQL Server to communicate with the remote Azure server. For more info about the requirements for this option, see [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
    -   **Create new server**  
  
        1.  Create a login and password for the server administrator.  
  
        2.  Optionally, use a federated service account for SQL Server to communicate with the remote Azure server.  
  
         ![Create new Azure server - Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-4.png "Create new Azure server - Stretch Database wizard")  
  
    -   **Existing server**  
  
        1.  Select the existing Azure server.  
  
        2.  Select the authentication method.  
  
            -   If you select **SQL Server Authentication**, provide the administrator login and password.  
  
            -   Select **Active Directory Integrated Authentication** to use a federated service account for SQL Server to communicate with the remote Azure server. If the selected server is not integrated with Azure Active Directory, this option doesn't appear.
  
         ![Select existing Azure server - Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-5.png "Select existing Azure server - Stretch Database wizard")  
  
##  <a name="Credentials"></a> Secure credentials  
 You have to have a database master key to secure the credentials that Stretch Database uses to connect to the remote database.  
  
 If a database master key already exists, enter the password for it.  
  
 ![Screenshot showing the Secure credentials page of the Stretch Database wizard with the Password text box empty.](../../sql-server/stretch-database/media/stretch-wizard-6b.PNG "Secure credentials page of the Stretch Database wizard")  
  
 If the database does not have an existing master key, enter a strong password to create a database master key.  
  
 ![Screenshot showing the Secure credentials page of the Stretch Database wizard with the New Password and Confirm Password text boxes populated.](../../relational-databases/tables/media/stretch-wizard-6.png "Secure credentials page of the Stretch Database wizard")  
  
 For more info about the database master key, see [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) and [Create a Database Master Key](../../relational-databases/security/encryption/create-a-database-master-key.md). For more info about the credential that the wizard creates,  see [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
##  <a name="Network"></a> Select IP address  
 Use the subnet IP address range (recommended), or the public IP address of your SQL Server, to create a firewall rule on Azure that lets SQL Server communicate with the remote Azure server.  
  
 The IP address or addresses that you provide on this page tell the Azure server to allow incoming data, queries, and management operations initiated by SQL Server to pass through the Azure firewall. The wizard doesn't change anything in the firewall settings on the SQL Server.  
  
 ![Select IP address page of the Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-7.png "Select IP address page of the Stretch Database wizard")  
  
##  <a name="Summary"></a> Summary  
 Review the values that you entered and the options that you selected in the wizard and the estimated costs on Azure. Then select **Finish** to enable Stretch.  
  
 ![Summary page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-8.png "Summary page of the Stretch Database wizard")  
  
##  <a name="Results"></a> Results  
 Review the results.  
  
 To monitor the status of data migration, see [Monitor and troubleshoot data migration &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
 ![Results page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-9.PNG "Results page of the Stretch Database wizard")  
  
##  <a name="KnownIssues"></a> Troubleshooting the wizard  
 **The Stretch Database wizard failed.**  
 If Stretch Database is not yet enabled at the server level, and you run the wizard without the system administrator permissions to enable it, the wizard fails. Ask the  system administrator to enable Stretch Database on the local server instance, and then run the wizard again. For more info, see [Prerequisite: Permission to enable Stretch Database on the server](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer).  
  
## Next steps  
 Enable additional tables for Stretch Database. Monitor data migration and manage Stretch-enabled databases and tables.  
  
-   [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) to enable additional tables.  
  
-   [Monitor and troubleshoot data migration &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) to see the status of data migration.  
  
-   [Pause and resume data migration &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Manage and troubleshoot Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Backup Stretch-enabled databases](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Restore Stretch-enabled databases](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## See Also  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
