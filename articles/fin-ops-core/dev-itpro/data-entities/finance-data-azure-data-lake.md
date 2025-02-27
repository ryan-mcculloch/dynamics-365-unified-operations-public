---
# required metadata

title: Finance and Operations apps data in Azure Data Lake
description: This topic explains how to configure your Finance and Operations apps environment so that it has a data lake.
author: MilindaV2
ms.date: 01/04/2021
ms.topic: article
ms.prod: 
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: NOINDEX, NOFOLLOW
audience: Developer, IT Pro
# ms.devlang: 
ms.reviewer: kfend

# ms.tgt_pltfrm: 
ms.custom: 96283
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: milindav
ms.search.validFrom: 2020-03-01
ms.dyn365.ops.version: Platform Update 34

---

# Finance and Operations apps data in Azure Data Lake

[!include [banner](../includes/banner.md)]

> [!NOTE]
> The **Export to Data Lake** feature is in public preview in the United States, Canada, United Kingdom, Europe, South East Asia, East Asia, Australia, and Japan regions. If your Finance and Operations environment is in any of those regions, you can enable this feature in your environment by using Microsoft Dynamics Lifecycle Services (LCS).
>
> In the coming months, Microsoft will enable this feature in additional regions, based on the demand. If your environment isn't in a region where the preview is enabled, [complete the survey and let us know](https://aka.ms/FnODataLakePreviewSurvey). You can also join a [preview Yammer group](https://www.yammer.com/dynamicsaxfeedbackprograms/#/threads/inGroup?type=in_group&feedId=32768909312&view=all). You can use the Yammer group to stay in contact and ask questions that will help you understand the feature. 

The **Export to Data Lake** feature lets you copy data from your Finance and Operations apps into your own data lake (Azure Data Lake Storage Gen2). The system lets you select the tables and entities that are included. After you select the data that you want, the system makes an initial copy. The system then keeps the selected data up to date by applying changes, deletions, and additions. After data changes in your Finance and Operations app instances, there might be a delay of a few minutes before the data is available in your data lake.

## Turn on the Export to Data Lake feature
Before you can use this feature, see [Configure export to Azure Data Lake](configure-export-data-lake.md).

## Select data

> [!NOTE]
> If the feature, **Export to Azure Data Lake** isn't available in the **Feature management** module in your environment, sign in to the environment and add the following to the URL in your browser address: &mi=DataFeedsDefinitionWorkspace. For example, https://ax123456.cloud.test.dynamics.com/?cmp=USMF&mi=DataFeedsDefinitionWorkspace.

You can select the tables and entities that should be staged in Data Lake.

1. In your environment, go to **System Administration** \> **Setup** \> **Export to Data Lake**.

    You can also open the **Export to Data Lake** page by using the search field on the navigation bar. Enter **Configure** in the search field. The search results should include a link to the page.

2. On the **Export to Data Lake** page, on the **Choose Tables** tab, select the data tables that should be staged in Data Lake. You can search for tables by either display name or system name. You can also see whether a table is being synced. 
3. When you've finished, select **Add Tables** to add the selected tables to Data Lake.

    ![Selecting tables](./media/Export-Table-to-Data-lake-Tables-Running-state.png)

4. Select **Activate data feed**, and then select **OK**. When you add a table, the system might show its status as **Initializing**. This status indicates that the system is making an initial copy of data. When the initial copy is completed, the system changes the status to **Running**.

    In the event of an error, the system shows the status as **Deactivated**.

    You can consume data in the data lake when the status is **Running**. If you consume data in the data lake while the status is **Initializing** or **Deactivated** status, you might not see all the data. 

    If you aren't familiar with the specific tables that you require, you can select tables by using entities. Entities are a higher-level abstraction of data and might include multiple tables. By selecting entities, you also select the tables that include them.

    > [!NOTE]
    > When you open the **Choose using Entities** tab for the first time, you might notice that the list of entities on the page is empty. The system might require some time to fill in the list of entities. You can force a refresh of the list by selecting **Manage \> Rebuild data feed catalog** on the Action Pane. 

5. On the **Choose using Entities** tab, select the entities, and then select **Add Tables using Entities**.

    ![Selecting tables by using entities](./media/Export-Table-to-Data-lake-Entities-Running-state.png)

    Regardless of the method that you use to select tables, the tables will be staged in Data Lake.

## Monitor the tables in Data Lake

You don't have to monitor or schedule data exports, because the system keeps the data updated in Data Lake. However, you can view the status of ongoing data exports in the **Status** column on the **Export to Data Lake** page.

## Troubleshooting common issues and errors

### Export to Data Lake feature is not available in your region and/or your environment at this time
This feature is not available in Tier-1 (developer) environments. You need a sandbox environment (Tier 2 or higher) with Platform updates for version 10.0.13 or higher.

This feature is in limited preview and may not be available in all Azure regions where Finance and Operations apps are available, or this feature may not be available for your environment. If you would like to join a future preview, [complete the survey](https://aka.ms/FnODataLakePreviewSurvey). We will contact you when we are ready to include you. You can also join a Yammer group by completing the survey. You can use the Yammer group to stay in contact and ask questions that will help you understand the feature. We are working hard to make this feature available soon.

### Export to Data Lake feature is currently being installed for your environment. Please check back later.
Before you can use this feature, you need to configure the export to Data Lake. For more information, see [Configure export to Azure Data Lake](configure-export-data-lake.md).

### Export to Data Lake add-in is not installed. 
Ask your administrator to install this add-in using Dynamics Lifecycle Services (LCS). Before you can use this feature, you need to configure the export to Data Lake. For more information, see [Configure export to Azure Data Lake](configure-export-data-lake.md).

### Export to Data Lake feature failed to install in Dynamics Life Cycle Services (LCS). 
Ask your administrator to re-install the Export to Data Lake add-in. If this issue persists, contact Support. When you configure the Export to Data Lake feature, the system may report an error. Or, there may be an error when you access the data lake after configuration due to a change in your environments. For more information, see [Configure export to Azure Data Lake](configure-export-data-lake.md).

### Export to Data Lake feature is temporarily unavailable. Please check back later.
If you see this error for a prolonged period of time, contact Support.  

### Status codes with extended errors
When an error occurs in a table that you added to Export to Data Lake, you may see an error code in the status column. The following error codes provide the cause of the error and how to correct the issue.

**Error status codes 4xx indicate an issue with the table** 

| Error code | Issue                                                                  | Next steps                                                                                                                                                                                                                                                                                                                                                                     |
|------------|-----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 400        | The table you added doesn't contain a RecID field.                   | RecID fields are used by the system to index table data. Tables that don't contain a RecID field can't be added to the Data Lake. If this issue is from a table in a Finance and Operations app, contact Microsoft support. If this table was developed by your partner or ISV, contact the developer to include a RecID field.                                  |
| 401        | The table you added is missing in the database. | The table you added is no longer available in the database and the system can't continue updating data in the lake. The table may have been removed because of a software or database update. Contact your database administrator or a developer. If this table was developed by your partner or ISV, contact the developer.                 |
| 402        | The RecID field isn't indexed.                                            | The system has detected that the RecID field contained in the table isn't part of an index. This may lead to poor performance in updating the data lake and updates may take longer to reflect in the data lake. If this issue is from a table in a Finance and Operations app, contact Microsoft support. If this table was developed by your partner or ISV, contact the developer. |

**Error status codes 5xx indicate a system error encountered while exporting data**
Due to the error, the system has paused data export – data that exists in the lake won't be updated until the error is resolved. Try to deactivate and activate the table to see if this resolves the issue. Note that deactivating and activating the table may cause the system to re-initialize the data in the lake by taking a full copy. If the issue persists, contact Microsoft support with the table name and the error code.

**Error status codes 8xx and 9xx indicate a change to the table or database structure since it was added**

| Error code | Issue                                                                                 | Next steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------|---------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 800        | There is a change in the data table schema.                                            | The system found a change in the table structure when adding changed data to the lake. This change is typically the result of a software update or a database modification. For example, when a new field is added to a table, or a field is modified or removed, the data updated in the lake may not be in the same format as the existing data. Because of the error, the system has paused data export. The data that exists in the lake won't be updated until the error is resolved. Deactivate and activate the table to see if the issue is resolved. |
| 801        | There is an issue with the Change data capture feature. | The Export to Data Lake feature uses the Change data capture feature. Change data can't be exported because the Change data capture feature is disabled in the Finance and Operations apps database. This may be the result of a database maintenance operation. Deactivate and activate the table to see if the issue is resolved. If the issue persists, contact Microsoft support.                                                                                                                                                                                          |
| 802        | There is an issue with the Change data capture feature for the table.                      | The Export to Data Lake feature uses the Change data capture feature. Change data can't be exported because the Change data capture feature isn't enabled for this table in your Finance and Operations apps database. This may be the result of a database maintenance operation. Deactivate and activate the table to see if the issue is resolved.                                                                                                                                                                         |
| 900        | There is an issue with the Change data capture feature in this environment.               | The Export to Data Lake feature uses the Change data capture feature. Change data can't be exported because the Change data capture feature isn't enabled for this table in the Finance and Operations apps database. This may be the result of a database maintenance operation. Deactivate and activate the table to see if the issue is resolved. If the issue persists, contact Microsoft support.                                                                                                                                                                        |


> [!NOTE]
> Deactivating and activating the table may cause the system to re-initialize the data in the lake by creating a full copy. If this is a large table, the initialize process may take some time. In the future, the system may automatically update data in the lake to reflect the table structure changes. 



[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
