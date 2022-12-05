---
title: SharePoint (preview)
description: SharePoint (preview) Actions Reference
author: georgiostrantzas
ms.subservice: desktop-flow
ms.topic: reference
ms.date: 11/22/2022
ms.author: gtrantzas
ms.reviewer: dipapa
contributors:
search.app: 
  - Flow
search.audienceType: 
  - flowmaker
  - enduser
---

# SharePoint (preview)

The SharePoint (preview) group of actions allows the utilization of the [SharePoint connector](/connectors/sharepointonline) from within desktop flows, alleviating the need to create a cloud flow in order to use its actions. This connector is the same as the one used across Power Automate cloud flows, PowerApps, and Logic Apps. It uses the same parameters and returns the same type of data.

## Prerequisites and limitations

- During preview, you need an Attended RPA license.

- Sharing desktop flows with SharePoint cloud actions isn't supported. Co-owners won't be able to run such desktop flows unless they overwrite the connection references with their own. **Users** with read access are unable to run such flows.

- Data loss prevention policies (DLP) that include SharePoint cloud actions aren't enforced within desktop flows. During preview, machine administrators can disable the SharePoint actions by modifying the [appropriate registry setting](../governance.md#prevent-power-automate-for-desktop-from-running-flows-containing-cloud-connectors).

- Refrain from modifying a response’s properties directly as it may lead to an erroneous state after future updates. Instead, opt for storing the properties you want to utilize (from the response retrieved) directly into separate variables.

## Why should I use SharePoint actions inside desktop flows instead of cloud flows?

Users can still combine SharePoint actions with the **Run a flow built with Power Automate for desktop** action. However, SharePoint actions inside desktop flows improve performance and ease of use for users who need to loop between cloud and desktop actions.

## List of SharePoint actions

- [Update file](#update-file)
- [Delete file](#delete-file)
- [Get file content using path](#get-file-content-using-path)
- [Get file content](#get-file-content)
- [Create file](#create-file)
- [List folder](#list-folder)
- [Get all lists and libraries](#get-all-lists-and-libraries)
- [Get file metadata](#get-file-metadata)
- [Get file metadata using path](#get-file-metadata-using-path)
- [Get folder metadata](#get-folder-metadata)
- [Get folder metadata using path](#get-folder-metadata-using-path)
- [List root folder](#list-root-folder)
- [Extract folder](#extract-folder)
- [Get lists](#get-lists)

## Getting started with SharePoint actions in desktop flows

This section presents examples on how to use SharePoint actions in your desktop flows.

### How to download the content of a SharePoint folder

> [!IMPORTANT]
> Before replicating the following steps, ensure that you are familiar with [lists](../variable-data-types.md#list), [custom objects](../variable-data-types.md#custom-object), [loops](../use-loops.md), [conditionals](../use-conditionals.md), and the [percentage notation](../variable-manipulation.md).

1. Ensure that you've installed the [latest version of Power Automate for desktop](../install.md).

1. Create a new desktop flow.

1. If the identifier of the target folder is unknown, use the **Get folder metadata using path** SharePoint action to retrieve it. This action requires the folder's path and produces a custom object containing the folder's metadata. You can access the identifier using the **Id** property.

    :::image type="content" source="media\sharepoint\sharepoint-get-folder-metadata-using-path-action.png" alt-text="Screenshot of the Get folder metadata using path action.":::

1. Deploy the **List folder** SharePoint action and populate the appropriate SharePoint URL and the previously retrieved identifier. The produced list contains custom objects representing items in the target folder.

    :::image type="content" source="media\sharepoint\sharepoint-list-folder-action.png" alt-text="Screenshot of the List folder action.":::

1. After retrieving the list, use a **For each** loop to iterate through the objects inside it.

    :::image type="content" source="media\sharepoint\for-each-action.png" alt-text="Screenshot of the For each loop that iterates through the retrieved custom objects.":::

1. If the items in the target folder are only files, use the Get file content using path action, and the **Path** property inside the block to retrieve the current file's contents.

    :::image type="content" source="media\sharepoint\sharepoint-get-file-content-using-path-action.png" alt-text="Screenshot of the Get file content using path action.":::

1. Then, deploy the **Convert binary data to file** action to store the retrieved data in a local file. You can use the **Name** property to name the new file with the same name as the original SharePoint file.

    :::image type="content" source="media\sharepoint\convert-binary-data-file-action.png" alt-text="Screenshot of the Convert binary data to file action.":::

The previous steps cover the case where the target folder contains only files. However, if the folder contains subfolders with files inside them, modify your desktop flow accordingly:

1. Add an **If** condition inside the previously deployed loop to check whether the currently selected item is a folder. To perform this check, use the **IsFolder** property of the current item.

    :::image type="content" source="media\sharepoint\if-action-folder.png" alt-text="Screenshot of the if action that checks whether the current item is a folder.":::

1. Inside the if-block, use the **Get folder metadata using path** action to get the identifier of the currently selected folder. The folder path is the same as the one you used at the beginning of the flow, plus the folder's name. You can access the folder using the **Name** property of the current item.

    :::image type="content" source="media\sharepoint\sharepoint-get-folder-metadata-using-path-actio-name-property.png" alt-text="Screenshot of the second Get folder metadata using path action.":::

1. As you did before, deploy the **List folder** SharePoint action and populate the appropriate SharePoint URL and the previously retrieved identifier.

    :::image type="content" source="media\sharepoint\sharepoint-list-folder-action-second.png" alt-text="Screenshot of the second List folder action.":::

1. Deploy a **For each** loop to iterate through the files inside the selected subfolder, and move and modify the previously deployed **Get file content using path** and **Convert binary data to file** actions to retrieve and save locally the contents of each file.

    :::image type="content" source="media\sharepoint\final-flow.png" alt-text="Screenshot of the final flow.":::

If you want to download files of specific subfolders, modify the previously deployed conditional to check the desired condition. For example, the following condition checks whether the current item's name is any other than 2022.

> [!NOTE]
> Although you could use a new nested **If** action, combining the checks in only one conditional makes the desktop flow less complicated and easier to read.

:::image type="content" source="media\sharepoint\if-action-item-name.png" alt-text="Screenshot of a conditional that checks the current item's name.":::

If you want to download only files of a specific type, add a conditional before retrieving the file contents to check whether the file name ends with a particular extension.

:::image type="content" source="media\sharepoint\if-action-item-type.png" alt-text="Screenshot of a conditional that checks the current item's file type.":::

### How to upload a local file to SharePoint

1. Ensure that you've installed the [latest version of Power Automate for desktop](../install.md).

1. Create a new desktop flow.

1. Deploy the **Convert file to binary data** action and select the desired file on your local drive. The action stores the converted file in the **BinaryData** variable.

    :::image type="content" source="media\sharepoint\convert-file-binary-data-action.png" alt-text="Screenshot of the Convert file to binary data action.":::

1. Find the **SharePoint (preview)** group of actions in the flow designer and deploy the **Create file** action in the workspace.

1. Select an existing connection reference and fill in the required parameters. Here's an example about how to fill the fields:

      > [!IMPORTANT]
      > Don't forget to add the appropriate file extension after the file name.

    :::image type="content" source="media\sharepoint\sharepoint-create-file-action.png" alt-text="Screenshot of the Create file Sharepoint action.":::

## How to fill action’s input fields

Until dynamic suggestions of input fields become available, here's guidance on what data to fill in for each action.

> [!NOTE]
> Another way to see which properties are expected as input and output is to create a cloud flow with the same action and observe its dynamic data properties. To find more information regarding the SharePoint cloud actions, refer to [SharePoint](/connectors/sharepointonline).

### Update file

Updates the contents of the file specified by the file identifier.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Identifier    |id              |True     |String |The unique ID of the file to select.                                                             |
|File Content       |body            |True     |Binary |The content of the file.                                                                         |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                  |

### Delete file

Deletes the file specified by the file identifier.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Identifier    |id              |True     |String |The unique ID of the file to select.                                                             |

### Get file content using path

Gets file contents using the file path.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Path          |path            |True     |String |The path of the target file, for example: "/Shared Documents/MyFolderName/myfilename.xlsx".       |
|Infer Content Type |inferContentType|         |Boolean|This parameter isn't needed when using the **Get file content using path** action in desktop flows, as the maker can define the file extension to use with the **Convert binary data to file** action. |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|File Content |FileContent  |Binary    |The content of the file in binary format.                               |

### Get file content

Get file contents using the file identifier. The contents can be copied somewhere else, or be used as an attachment.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Identifier    |id              |True     |String |The unique ID of the file to select.                                                             |
|Infer Content Type |inferContentType|         |Boolean|This parameter isn't needed when using the **Get file content using path** action in desktop flows, as the maker can define the file extension to use with the **Convert binary data to file** action. |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|File Content |FileContent  |Binary    |The content of the file in binary format.                               |

### Create file

Uploads a file to a SharePoint site. Make sure to pick an existing library.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|Folder Path        |folderPath      |True     |String |Must start with an existing library. Add folders if needed.                                      |
|File Name          |name            |True     |String |The name of the file.                                                                            |
|File Content       |body            |True     |Binary |The content of the file.                                                                         |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|ItemId       |ItemId       |Integer   |The value to use to get or update file properties in libraries.         |
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                  |

### List folder

Returns files contained in a SharePoint folder.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Identifier    |id              |True     |String |The unique ID of the folder.                                                                     |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                  |

### Get all lists and libraries

Get all lists and libraries.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |

#### Returns

|Name         |Path         |Type            |Description                                                             |
|-------------|-------------|----------------|------------------------------------------------------------------------|
|value        |value        |array of Tables |List of Tables                                                          |

### Get file metadata

Gets information about the file such as size, etag, created date, etc. Uses a file identifier to pick the file. Use **Get file properties** action to get to the values stored in the columns in the library.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Identifier    |id              |True     |String |The unique ID of the folder.                                                                     |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|ItemId       |ItemId       |Integer   |The value to use to get or update file properties in libraries.         |
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                 |

### Get file metadata using path

Gets information about the file such as size, etag, created date, etc. Uses a file path to pick the file. Use **Get file properties** action to get to the values stored in the columns in the library.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Path          |path            |True     |String |The path of the target file, for example: "/Shared Documents/MyFolderName/myfilename.xlsx".       |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|ItemId       |ItemId       |Integer   |The value to use to get or update file properties in libraries.         |
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                 |

### Get folder metadata

Gets information about the folder. Uses a file identifier to pick the folder.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|File Identifier    |id              |True     |String |The unique ID of the folder.                                                                     |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|ItemId       |ItemId       |Integer   |The value to use to get or update file properties in libraries.         |
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                 |

### Get folder metadata using path

Gets information about the folder. Uses a folder path to pick the folder.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|Folder Path        |path            |True     |String |The path of the target folder, for example: "/Shared Documents/MyFolderName.                      |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|ItemId       |ItemId       |Integer   |The value to use to get or update file properties in libraries.         |
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                 |

### List root folder

Returns files in the root SharePoint folder.

#### Parameters

|Name               |Key             |Required |Type   |Description                                                                                      |
|-------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address       |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|ItemId       |ItemId       |Integer   |The value to use to get or update file properties in libraries.         |
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                 |

### Extract folder

Extracts an archive file into a SharePoint folder (example: zip).

|Name                    |Key             |Required |Type   |Description                                                                                      |
|------------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address            |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |
|Source File Path        |source          |True     |String |The path of the source file.                                                                      |
|Destination Folder Path |destination     |True     |String |The path of the destination folder.                                                              |
|Overwrite Flag          |overwrite       |         |BooleanSpecifies whether to overwrite the destination file if it exists.                                 |

#### Returns

|Name         |Path         |Type      |Description                                                             |
|-------------|-------------|----------|------------------------------------------------------------------------|
|ItemId       |ItemId       |Integer   |The value to use to get or update file properties in libraries.         |
|Id           |Id           |String    |The unique ID of the file or folder.                                    |
|Name         |Name         |String    |The name of the file or folder.                                         |
|DisplayName  |DisplayName  |String    |The display name of the file or folder.                                 |
|Path         |Path         |String    |The path of the file or folder.                                         |
|LastModified |LastModified |Date-time |The date and time the file or folder was last modified.                 |
|Size         |Size         |Integer   |The size of the file or folder.                                         |
|MediaType    |MediaType    |String    |The media type of the file or folder.                                   |
|IsFolder     |IsFolder     |Boolean   |A boolean value (true, false) to indicate whether the blob is a folder. |
|ETag         |ETag         |String    |The etag of the file or folder.                                         |
|FileLocator  |FileLocator  |String    |The file locator of the file or folder.                                 |

### Get lists

Gets SharePoint lists from a site.

#### Parameters

|Name                    |Key             |Required |Type   |Description                                                                                      |
|------------------------|----------------|---------|-------|-------------------------------------------------------------------------------------------------|
|Site Address            |dataset         |True     |String |The URL of the SharePoint site, for example: <br>'https://contoso.sharepoint.com/sites/sitename'. |

#### Returns

|Name         |Path         |Type            |Description                                                             |
|-------------|-------------|----------------|------------------------------------------------------------------------|
|value        |value        |array of Tables |List of Tables                                                          |

## Upcoming features

- Dynamic content for output variables: cloud actions’ output variables can be expanded to show its underlying properties
- Share to **users** brings their own connection references upon each run
- Co-owners can use the same connection references
- ALM dependencies management (dependency checker upon import, add required objects, show dependencies)
- Connection references are visible in desktop flows details pages
- Exponential/manual retry policies in case the connector responds an error
- DLPs that include SharePoint cloud actions are enforced in desktop flows
- New SharePoint actions
