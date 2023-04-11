---
title: Turn flows on or off in Power Automate | Microsoft Docs
description: Learn how to turn flows on or off in Power Automate.
services: ''
suite: flow
documentationcenter: na
author: puyush6889
ms.subservice: cloud-flow
ms.topic: conceptual
ms.date: 06/14/2022
ms.author: kapolepa
ms.reviewer: angieandrews
search.audienceType:
  - flowmaker
  - enduser
---

# Turn flows on or off

At times, you might want to turn off a cloud flow to prevent it from running. Follow these steps to turn flows off or on.

## Turn flows off

After you create a cloud flow, it's turned on by default. Follow these steps to turn off a cloud flow.

1. On the left pane, select **My Flows**.

1. Select a cloud flow, and then select **More commands** (...) icon.

    >[!div class="mx-imgBorder"]
    >![Screenshot of the More commands icon.](./media/disable-flow/flows-collapsed-menu.png "More commands icon")
    
1. On the menu that appears, select **Turn off**. <!--Note from Sweeny: Can we add the screenshot here as well for more clarity-->

1. On the **Details** page, select the **More commands** (...) icon, and then select **Details** to Verify the new status.

    >[!div class="mx-imgBorder"]
    >![Screenshot of flow status on Details page.](./media/disable-flow/flow-details-page-new-status.png "Flow status on the Details page")

>[!NOTE]
>If you turn off a flow, its runs are queued and they'll run when you turn the flow on.

## Turn flows on

If you've turned off a cloud flow, but want to turn it back on so that it will run again, follow one of these steps.

- If you are on the **Details** page, in the menu at the top, select **Turn on**.

    >[!div class="mx-imgBorder"]
    >![Screenshot of the 'Turn on' menu option.](./media/disable-flow/flow-details-page-new-status-on.png "'Turn on' menu option")

- If you are on the **Flows** page:

    1. Select a cloud flow, and then select **More commands** (...) icon.

    1. On the menu that appears, select **Turn on**. The status changes to **On**.

>[!NOTE]
>If you disable a flow while it's running, the run will continue. If you delete a flow that's running, the current run terminates.

[!INCLUDE[footer-include](includes/footer-banner.md)]
