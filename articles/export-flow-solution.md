---
title: Learn how to export solution-aware flows | Microsoft Docs
description: Learn how to export solution-aware flows.
services: ''
suite: flow
documentationcenter: na
author: msftman
manager: kvivek

ms.subservice: cloud-flow
ms.topic: article
ms.date: 06/09/2022
ms.author: deonhe
ms.reviewer: angieandrews
search.app: 
  - Flow
search.audienceType: 
  - flowmaker
  - enduser
---

# Export a solution

Follow these steps to move your solution and its dependencies to a new environment.

>[!IMPORTANT]
>Before you export a solution, consider removing environment variable values in the solution.

1. Sign into [Power Automate](https://make.powerautomate.com).

1. Select **Solutions** from the navigation bar on the left side of Power Automate.

1. Select the unmanaged solution that you want to export.

1. Select **Export** from the menu at the top of the screen.

1. The **Before you export** right pane appears. Choose from the following options.
    - **Publish all changes** - Notice that, when you export an unmanaged solution, only published components are exported. We recommend that you select **Publish** to confirm that all components are in the exported solution.
    - **Check for issues** - Run the solution checker against the solution to detect performance and stability issues.

1. Select **Next**.

1. The **Export this solution** page appears on the right. Enter or select from the following options, and then select **Export**.  
    - **Version number** - Power Automate automatically increments your solution version. You can accept the default version or enter your own.
    - **Export as** - Select the package type, either **Managed** or **Unmanaged**. More information: [Managed and unmanaged solutions](/power-platform/alm/solution-concepts-alm#managed-and-unmanaged-solutions)

The export can take several minutes to complete. After the export finishes, the exported solution zip file is available in the downloads folder for your web browser.

Find the flows within the **Workflows** folder in the solution zip file. Each exported workflow is represented as a JSON file. Flow definitions were traditionally a compact block of JSON in a single line, but in February 2022 the export format was changed to multi-line formatted JSON to make them easier to read and make them friendlier to revision tracking in source control.

## Tips

- You can also find your solutions via the **Solutions** card in the flow details page of solution-aware cloud flows. Alternatively, select the solution in which your are interested from the **Solutions** card, select the **Overview** tab, and then use the **Export** button there.

- You can't export managed solutions. More information: [Managed and unmanaged solutions](/power-platform/alm/solution-concepts-alm#managed-and-unmanaged-solutions)

- Once a flow is solution-aware and in Dataverse, you must use the steps in this article to export it. You cannot export a solution-aware cloud flow from the flow details page.

- To implement healthy application lifecycle management (ALM) in your organization, use a source control system to store and collaborate on your solutions, and automate the solution export process. More information: [ALM basics](/power-platform/alm/basics-alm) in the Power Platform ALM guide.

## Learn more

- [Create a solution](./overview-solution-flows.md)
- [Create a cloud flow in a solution](./create-flow-solution.md)
- [Import a solution](./import-flow-solution.md)
- [Edit a solution-aware flow](./edit-solution-aware-flow.md)
- [Environment variables overview](/powerapps/maker/data-platform/environmentvariables)

[!INCLUDE[footer-include](includes/footer-banner.md)]
