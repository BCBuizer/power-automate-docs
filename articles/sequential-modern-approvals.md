---
title: Manage sequential approvals with Power Automate
description: 'Create a modern approval workflow with multiple approvers '
services: ''
suite: flow
documentationcenter: na
author: MSFTMan
editor: ''
tags: ''

ms.devlang: na
ms.subservice: cloud-flow
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/13/2020
ms.author: deonhe
ms.reviewer: gtrantzas
ms.collection: get-started
search.audienceType: 
  - flowmaker
  - enduser
---
# Manage sequential approvals with Power Automate

Some workflows require pre-approval before the final approver is required to sign off. For example, a company may have a sequential approval policy that requires pre-approval for invoices over $1000.00 before they're approved by the Finance department.

In this tutorial, you create a sequential approval flow that manages employee vacation requests. For detailed information about using SharePoint with Power Automate, go to the SharePoint documentation.

For detailed information about using SharePoint with Power Automate, go to the [SharePoint documentation](/sharepoint/dev/business-apps/power-automate/sharepoint-connector-actions-triggers).

> [!NOTE]
> SharePoint is used here only as an example. It isn't required to create approval flows. You can use any of the more than 200 services with which Power Automate integrates to drive your flows. If you're using SharePoint 2010, go to [SharePoint 2010 workflow retirement](https://go.microsoft.com/fwlink/?linkid=2138686).

## Detailed steps in the flow

The flow:

1. Starts when an employee creates vacation request in a [SharePoint Online list](https://support.office.com/article/Introduction-to-lists-0a1c3ace-def0-44af-b225-cfa8d92c52d7).
1. Adds the vacation request to the approval center and then emails the request to the pre-approver.
1. Emails the pre-approval decision to the employee.
1. Updates the SharePoint Online list with the pre-approver's decision and comments.
   Note: If the request is pre-approved, the flow continues with these steps:
1. Sends the request to the final approver.
1. Emails the final decision to the employee.
1. Updates the SharePoint list with the final decision.

This image summarizes the preceding steps:

   ![Diagram of sequential approval flow.](./media/sequential-modern-approvals/visio-overview.png)

## Prerequisites

[!INCLUDE [prerequisites-for-modern-approvals](includes/prerequisites-for-modern-approvals.md)]

For the purposes of this walkthrough, the SharePoint Online list that you create must include the following columns:

The SharePoint Online list you create must include the following columns:

| Title                   | Single line of text    |
|-------------------------|------------------------|
| Vacation start date     | Date and time          |
| Vacation end date       | Date and time          |
| Comments                | Single line Of text    |
| Approved                | Yes/No                 |
| Manager comments        | Multiple lines Of text |
| Modified                | Date and time          |
| Created                 | Date and time          |
| Pre-approved            | Yes/No                 |
| Created By              | Person or group        |
| Modified By             | Person or group        |

Make  note of the name and URL of the SharePoint Online list. We use these items later when you configure the **SharePoint - When a new item is created** trigger.

Power Automate uses either the classic designer or the Edit with Copilot (preview) designer. To identify which designer you’re using, go to the **Note** section in [Understand the Edit with Copilot designer (preview)](../flows-designer.md).

## Create your flow

# [Classic designer](#tab/classic-designer)

[!INCLUDE [sign-in-and-create-flow-from-blank-template](includes/sign-in-and-create-flow-from-blank-template.md)]

[!INCLUDE [add-trigger-when-sharepoint-item-created](includes/add-trigger-when-sharepoint-item-created.md)]

1. On the **When an item is created** card, select the **Site Address** and the **List Name** for the SharePoint list that you created earlier.

   ![sharepoint info.](./media/sequential-modern-approvals/select-sharepoint-site-info.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Get the manager for the person who created the vacation request

# [Classic designer](#tab/classic-designer)

[!INCLUDE [add-get-manager-action](includes/add-get-manager-action.md)]

   > [!NOTE]
   > It's a good idea to periodically save changes to your flow as you go.

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Add an approval action for pre-approvals

# [Classic designer](#tab/classic-designer)

[!INCLUDE [add-an-approval-action](includes/add-an-approval-action.md)]

This action sends the pre-approval request to the email address in the **Assigned To** box.

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Add a condition

# [Classic designer](#tab/classic-designer)

[!INCLUDE [add-approval-condition-response](includes/add-approval-condition-response.md)]

> [!NOTE]
> This condition checks the response from the **Start and wait for an approval** action.

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Add an email action for pre-approvals

# [Classic designer](#tab/classic-designer)

[!INCLUDE [add-action-to-send-email-when-vacation-approved](includes/add-action-to-send-email-when-vacation-approved.md)]

   ![configure pre-approved email template.](./media/sequential-modern-approvals/yes-email-config.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Add an update action for pre-approved requests

# [Classic designer](#tab/classic-designer)

[!INCLUDE [add-action-to-update-sharepoint-with-approval](includes/add-action-to-update-sharepoint-with-approval.md)]

   ![update an item configuration.](./media/sequential-modern-approvals/update-item-preapproval.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Get the pre-approver's manager

# [Classic designer](#tab/classic-designer)

1. Use the [Get the manager for the person who created the vacation request](sequential-modern-approvals.md#get-the-manager-for-the-person-who-created-the-vacation-request) steps we did earlier to add, and then configure another **Get manager** action. This time we get the pre-approver's manager.
2. The **Get manager 2** card should resemble this image when you're finished. Be sure to use the **Email** token from the **Get manager** category on the **Add dynamic content from the apps and services used in this flow** card.

   ![get pre-approver's manager.](includes/media/modern-approvals/get-pre-approver-manager.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Add the final approval action

# [Classic designer](#tab/classic-designer)

1. Use the [add an approval action for pre-approvals](sequential-modern-approvals.md#add-an-approval-action-for-pre-approvals) steps we did earlier to add, and then configure another **Start and wait for an approval** action. This action sends an email request for final approval.
2. When you're done, the card should resemble this image:
   
    ![configure the approval.](./media/sequential-modern-approvals/provide-approval-config-info.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---
## Add the final approval condition

# [Classic designer](#tab/classic-designer)

1. Repeat the steps from [add a condition](sequential-modern-approvals.md#add-a-condition) to add, and then configure a **Condition** that checks the final approver's decision.

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Send email with final approval

# [Classic designer](#tab/classic-designer)

1. Use the steps from [Add an email action for pre-approvals](sequential-modern-approvals.md#add-an-email-action-for-pre-approvals) to add, and then configure an action that sends an email when vacation requests are approved.
2. When you're finished, your card should resemble this image:
   
   ![final approval email template.](./media/sequential-modern-approvals/vacatioin-request-approved-email-template.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Update SharePoint with approval

# [Classic designer](#tab/classic-designer)

1. Use the steps from [Add an update action for pre-approved requests](sequential-modern-approvals.md#add-an-update-action-for-pre-approved-requests) to add, and then configure an action that updates SharePoint when the vacation request is approved.
2. When you're finished, the card should resemble this image:
   
    ![update item configuration card.](./media/sequential-modern-approvals/configure-update-item-approved.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Send email with pre-approval rejection

# [Classic designer](#tab/classic-designer)

[!INCLUDE [add-action-to-send-email-when-vacation-rejected](includes/add-action-to-send-email-when-vacation-rejected.md)]

   ![configuration for rejected requests.](./media/sequential-modern-approvals/configure-rejected-email.png)

This action must be added to the **IF NO, DO NOTHING** branch below the **Condition** card.

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Update SharePoint with pre-approval rejection

# [Classic designer](#tab/classic-designer)

[!INCLUDE [add-action-to-update-sharepoint-with-rejection](includes/add-action-to-update-sharepoint-with-rejection.md)]

   ![update sharepoint for rejected requests.](./media/sequential-modern-approvals/update-sharepoint-with-rejection.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Send email with final rejection

# [Classic designer](#tab/classic-designer)

1. Use the steps from [Send email with pre-approval rejection](sequential-modern-approvals.md#send-email-with-pre-approval-rejection) to add, and then configure an action that sends an email when the vacation request is rejected by the final approver.

    This action must be added to the **IF NO, DO NOTHING** branch below the **Condition 2** card.

1. When you're finished, the card should resemble this image:

   ![Screenshot of the configuration for rejected requests.](./media/sequential-modern-approvals/final-rejection-email-card.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Update SharePoint with final rejection

# [Classic designer](#tab/classic-designer)

1. Use the steps from [Update SharePoint with pre-approval rejection](sequential-modern-approvals.md#update-sharepoint-with-pre-approval-rejection) to add, and then configure an action that updates SharePoint if the final approver rejects the vacation request.
1. When you're finished, the card should resemble this image:

   ![update item card.](./media/sequential-modern-approvals/final-rejection-update-sharepoint.png)
1. Select **Update flow** to save the work we've done.

If you've followed along, your flow should resemble this image:

![overview of flow.](./media/sequential-modern-approvals/completed-flow.png)

Now that you've created the flow, let's see it in action.

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Request an approval

# [Classic designer](#tab/classic-designer)

[!INCLUDE [request-vacation-approval](includes/request-vacation-approval.md)]

Your request should resemble this image:

![vacation request.](./media/sequential-modern-approvals/vacation-request.png)

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## View pending approval requests

# [Classic designer](#tab/classic-designer)

[!INCLUDE [view-pending-approvals](includes/view-pending-approvals.md)]

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Pre-approve a request

# [Classic designer](#tab/classic-designer)

[!INCLUDE [approve-request-from-different-locations](includes/approve-request-from-different-locations.md)]

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

---

## Approve the request

# [Classic designer](#tab/classic-designer)

The steps to approve a request are identical to the steps to [pre-approve a request](sequential-modern-approvals.md#pre-approve-a-request)

The final approver gets the vacation request only after the request has been pre-approved.

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](../includes/cc-beta-prerelease-disclaimer.md)]

---

## Reject a request

# [Classic designer](#tab/classic-designer)

[!INCLUDE [reject-a-request](includes/reject-a-request.md)]

# [Edit with Copilot (preview)](#tab/edit-with-copilot)

[!INCLUDE [cc-beta-prerelease-disclaimer](../includes/cc-beta-prerelease-disclaimer.md)]

---

### See also

[Single approver modern approvals walkthrough](modern-approvals.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
