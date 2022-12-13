---
title: Migration to Manifest V3 
description: See information about the deprecation of Manifest V2 and migration to Manifest V3.
author: georgiostrantzas
ms.subservice: desktop-flow
ms.topic: article
ms.date: 12/13/2022
ms.author: gtrantzas
ms.reviewer: nimoutzo
contributors:
search.app: 
  - Flow
search.audienceType: 
  - flowmaker
  - enduser
---

# Migration to Manifest V3

After June 2023, Google Chrome and Microsoft Edge browsers will no longer run Manifest V2 extensions. Currently, the Power Automate browser extensions for both browsers are based on Manifest V2. Therefore, the web extensions must be migrated to Manifest V3 to be functional after June 2023.

A manifest file is the blueprint of an extension. It includes information such as the version number and the title of the extension and permissions it needs to run. Migrating from Manifest V2 to V3 will bring several structural changes to how browsers handle the extensions. Manifest V3 extensions enjoy enhancements in security, privacy, and performance. They can also use more contemporary open web technologies such as service workers and promises.

## Plan of Manifest V2 deprecation

| Timeframe | Microsoft Partner Center and Chrome Web Store changes | Microsoft Edge and Google Chrome changes |
|-----------|-------------------------------------------------------|------------------------------------------|
| July 2022 | They'll no longer accept new Manifest V2 extensions with visibility set as Hidden or Public. | No change |
|June 2023 (Google Chrome) <br> TBD (Microsoft Edge) |They'll no longer accept updates to existing Manifest V2 extensions. Developers can submit updates for migrating a V2 extension to V3. |Both browsers will stop running Manifest V2 extensions. Enterprises can allow Manifest V2 extensions to run on both browsers using Enterprise policies. |
|January 2024 (Google Chrome) <br> TBD (Microsoft Edge) |No change | Manifest V2 extensions will no longer function in both browsers even with the use of Enterprise policy. |

Chromium has revised the timelines for Manifest V2 sunset. We'll independently decide on Manifest V3 migration timelines for Microsoft Edge Add-ons and share an update in this article. We continue to analyze the concerns raised by the extension developers and explore the optimal path for the Microsoft Edge Add-ons ecosystem. Meanwhile, refer to the [Chromium timelines](https://developer.chrome.com/docs/extensions/mv3/mv2-sunset) for planning your extension's migration.

To find more information, go to:

- [Manifest V2 support timeline](https://developer.chrome.com/docs/extensions/mv3/mv2-sunset/)
- [Overview and timelines for migrating to Manifest V3](/microsoft-edge/extensions-chromium/developer-guide/manifest-v3)

## Power Automate plan for deprecate Manifest V2 and migrate to V3

A new browser extension will be released in December 2022, with the name **Microsoft Power Automate**. The extension follows the Manifest V3 standard, taking advantage of its benefits. The new extension is compatible with Power Automate for desktop v2.27 (December 2022 release) or later. After June 2023, you should upgrade to Power Automate for desktop v2.27 (or later) and install the new extension.

The old web extension will continue to exist after the release of the new one. It will be renamed to **Microsoft Power Automate (Legacy)** and continue using Manifest V2. If you want to keep Power Automate for desktop v2.26 or older installed, use the legacy web extension until the end of May 2023.  

After June 2023, enterprise users have two options:

- Upgrade to Power Automate for desktop v2.27 or later and use the new browser extension.

- (Only for enterprises) Use Enterprise policies to allow Manifest V2 extensions to run on Microsoft Edge/Google Chrome. By enabling it, you may use Power Automate for desktop v2.26 or older and the legacy web extension until January 2024. After January 2024, everyone must upgrade to Power Automate for desktop v2.27 or later.

After June 2023, non-enterprise users must upgrade to Power Automate for desktop v2.27 or later and use the new browser extension.

## Run JavaScript function on web page action

> [!IMPORTANT]
> Due to security limitations issued by Mozilla Firefox, you can't use the **Run JavaScript function on web page** action with an instance of it. To utilize this action, use one of the other browser options in your desktop flow.

Due to limitations in the way Manifest V3 works, injecting JavaScript on a web page is impossible when Developer tools are disabled by Group Policy, making the action not functional.

If you upgrade to Power Automate for desktop v2.27 or later and use the new browser extension, the **Run JavaScript function on web page** action will be functional with the use of its debugger capability.

The action won't be impacted if you use the legacy browser extension and Power Automate for desktop v2.26 or older.

When the action runs, you'll see a  **"Microsoft Power Automate" started debugging this browser** message with no real effect on the execution.

> [!NOTE]
> The new version of the browser extension requires the browsers' Developer tools to be enabled. The extension uses its debugger capabilities to run the JavaScript code of the respective action.

To ensure that Developer tools aren't disabled in Microsoft Edge, go to [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies#developertoolsavailability).

To ensure that Developer tools aren't disabled in GoogleChrome, go to [Chrome Enterprise policy](https://chromeenterprise.google/policies/#DeveloperToolsAvailability).

## Upgrade to Power Automate for desktop v2.27 (or later) and the new browser extension

When the December 2022 release of Power Automate for desktop is available, you'll be able to download and upgrade as usual.

The new browser extensions will be installed automatically during Power Automate installation. If you want to install them manually, go to [Install Power Automate browser extensions](install-browser-extensions.md).

## Extend the usage of Manifest V2 extensions

If you want to wait to install the new version of the browser extension, you can extend the use of the Manifest V2 extensions until January 2024. You can extend the use through an enterprise group policy. However, by January 2024, you'll have to upgrade to the new version of the extension.

Google hasn't announced officially yet the way to enable the enterprise policy.

[!INCLUDE[footer-include](../includes/footer-banner.md)]
