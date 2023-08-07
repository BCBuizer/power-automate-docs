﻿---
title: Use your own Azure Data Lake Storage Gen2 (preview)
description: Learn how to store and read event log data directly from Azure Data Lake Storage Gen2.
author: HeatherOrt
contributors:
  - HeatherOrt
  - v-aangie 
ms.subservice: process-advisor
ms.topic: conceptual
ms.date: 08/08/2023
ms.custom: bap-template
ms.author: heortaol
ms.reviewer: angieandrews
---

# Use your own Azure Data Lake Storage Gen2 (preview)

[!INCLUDE[cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

Power Automate Process Mining gives you the option to store and read event log data directly from [Azure Data Lake Storage Gen2](/azure/storage/blobs/data-lake-storage-introduction). This feature simplifies extract, transform, load (ETL) management by connecting directly to your storage account.

> [!IMPORTANT]
> [!INCLUDE[cc_preview_features_definition](includes/cc-preview-features-definition.md)]

## Prerequisites

- The Data Lake Storage account must be Gen2. Azure Data Lake Gen1 storage accounts aren't supported.
- The Data Lake Storage account must have [hierarchical namespace](/azure/storage/blobs/data-lake-storage-namespace) enabled.
- The **Owner** role must be attributed to the user performing the initial container setup for the environment for the following users in the same environment. These users are connecting to the same container and must have the **Storage Account Contributor** role assigned.

- The Cross-Origin Resource Sharing (CORS) rule is established to share with Power Automate Process Mining.
    - Allowed origins must be established to `make.powerautomate.com`.
    - Allowed methods must include: `get`, `options`, `put`.
    - Allowed headers should be as flexible as possible. We recommend defining them as `\*`.
    - Exposed headers should be as flexible as possible. We recommend defining them as `\*`.
    - The maximum age should be as flexible as possible. We recommend using `86400`.

-   Data in your Data Lake Storage should meet the following CSV file format requirements:

    - **Compression type:** None
    - **Column delimiter:** Comma (,)
    - **Row delimiter:** Default and encoding. For example, Default (\r,\n, or \r\n) 

    :::image type="content" source="media/process-mining-byo-azure-data-lake/csv.png" alt-text="Screenshot of the File format settings screen.":::

- All data must be in final event log format and meet the requirements listed in [Data requirements](process-mining-processes-and-data.md#data-requirements). Data should be ready to be mapped to the process mining schema. No data transformation is available post ingestion.

> [!IMPORTANT]
> Ensure that time stamp represented in your CSV file follows the ISO 8601 standard format (for example, `YYYY-MM-DD HH:MM:SS.sss` or `YYYY-MM-DDTHH:MM:SS.sss`.

## Connect to Azure Data Lake Storage

1. On the navigation pane to the left, select **Process mining** > **Start here**.
1. In the **Process name** field, enter a name for your process.
1. Under the **Data source** heading, select **Import data** > **Azure Data Lake (preview)** > **Continue**.
1. On the **Azure Account Information** screen, select your Azure account information from the dropdown menus.
1. Select the file or folder containing the event log data.

    You can either select a single file or a folder with multiple files. All files must have the same headers and format.
1. Select **Next**.
1. On the **Map your data** screen, map your data to the required schema.

    :::image type="content" source="media/process-mining-byo-azure-data-lake/map.png" alt-text="Screenshot of the Map your data screen.":::

1. Complete the connection by selecting **Save and Analyze**.

## Define incremental refresh settings

You can refresh a process from Azure Data Lake on a schedule, either through a full or incremental refresh. Though there are no retention policies, you can ingest data incrementally using one of the following methods:

- Add incremental files to the selected folder.
- Append more data to the selected file.

> [!IMPORTANT]
> When you add incremental files to a selected folder or subfolder, make sure you indicate the increment order by naming files with dates such as YYYMMDD.csv or YYYYMMDDHHMMSS.csv.

To refresh a process:

1. Go to the **Details** page of the process.

1. Select **Refresh Settings**.

1. On the **Schedule refresh** screen, complete the following steps:

    1. Turn on the **Keep data up to date** toggle switch.
    1. In the **Refresh data every** dropdown lists, select the frequency of the refresh.
    1. In the **Start at** fields, select the date and time of the refresh.
    1. Turn on the **Incremental refresh (preview)** toggle switch.
