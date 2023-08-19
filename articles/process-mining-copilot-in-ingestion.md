﻿---
title: Copilot in Process Mining ingestion (preview)
description: Learn how to identify your process during data ingestion and auto map your data to the required data schema.
ms.date: 08/25/2023
ms.topic: conceptual
author: HeatherOrt
contributors:
  - HeatherOrt
  - v-aangie 
ms.custom: bap-template
ms.author: heortaol
ms.reviewer: angieandrews
---

# Copilot in Process Mining ingestion (preview)

[!INCLUDE[cc-preview-features-top-note](./includes/cc-preview-features-top-note.md)]

Copilot in Process Mining ingestion navigates you through the ingestion experience in Process Mining. With Copilot in Process Mining ingestion, you can identify your process during data ingestion and auto map your data to the required data schema.

Copilot can perform the following actions:

- Discover your process in your Azure Data Lake.
- Give automapping recommendations to required data schema.
- Answer your questions about your process data.
- Answer your general questions about processes.

>- [!INCLUDE[cc_preview_features_definition](./includes/cc-preview-features-definition.md)]
>- For more information, go to our [preview terms](https://powerplatform.microsoft.com/legaldocs/supp-powerplatform-preview/).
>- This capability is powered by [Azure OpenAI Service](/azure/cognitive-services/openai/overview).
>- More information: [FAQ for Copilot in Power Automate Process Mining](faqs-copilot-in-process-mining.md), [FAQ for Copilot data security and privacy in Power Platform](/power-platform/faqs-copilot-data-security-privacy)

## Prerequisites

You need a Power Platform environment in the United States or Preview (United States) region for Copilot in Process Mining.

> [!NOTE]
> If your environment is in the United States or Preview (United States) region and you still don’t see the Copilot experience, contact your admin. An admin can turn the Copilot feature off or on in the Power Platform admin center.

## Ingest Data with Copilot

Follow these steps to ingest data with Copilot.

1. Sign in to [Power Automate](https://powerautomate.com).
1. Select **Process mining** > **Start here** (under **Create new process**).
1. In the **Process name** field, enter a name for your process.
1. Under the **Data source** heading, select **Azure Data Lake (preview)**.
1. Select **Continue**.

    :::image type="content" source="media/process-mining-copilot-in-ingestion/new-process.png" alt-text="<alt text>":::

1. Complete the steps in the **Connection setup** screens for the Azure Data Lake container.
1. Select **Next**.

1. Select the folder or file you're interested in analyzing and Copilot identifies the process.
1. Confirm that it's the process you're interested in analyzing by selecting **Confirm process** > **Next**.

    :::image type="content" source="media/process-mining-copilot-in-ingestion/step-2.png" alt-text="Screenshot of the data source.":::

1. In the mapping screen, Copilot offers an automapping suggestion that you can review and choose to map your data to.

1. Once you've reviewed the automapping, you can save and analyze your process.

## Frequently asked questions

For the list of questions for Copilot in Process Mining ingestion, go to [Frequently asked questions](./minit/process-mining-copilot-in-process-analytics.md).

## Limitations of Copilot in Power Automate

For a list of limitations of Copilot in Power Automate, go to [Limitations of Copilot in Power Automate](minit/process-mining-copilot-in-process-analytics.md#limitations-of-copilot-in-power-automate).

### See also

- [Responsible AI FAQs for Power Automate](responsible-ai-overview.md)
- [FAQ for Copilot in Power Automate Process Mining](faqs-copilot-in-process-mining.md)
- [FAQ for Copilot data security and privacy in Microsoft Power Platform](/power-platform/faqs-copilot-data-security-privacy)
