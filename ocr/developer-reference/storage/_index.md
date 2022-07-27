---
weight: 30
date: "2022-07-21"
author: "Vladimir Lapin"
type: docs
url: /storage/
title: Working with cloud storage
description: How to access and manage Aspose.OCR Cloud storage and upload files to be recognized.
keywords:
- disk
- file
- folder
- storage
---

Aspose.OCR Cloud can extract text from images and scanned PDFs uploaded to the cloud storage.

## Adding a storage

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Storages**](https://dashboard.aspose.cloud/storages) page.
3. Click the **Create New Storage** button and select the type of online storage. You can either use one of the [third party storages](/total/getting-started/dashboard/how-to-configure-3rd-party-cloud-storages/) you already have or create a new storage in our cloud (_Internal Storage_).
4. Go to [**Applications**](https://dashboard.aspose.cloud/applications) page.
5. Click an application and select the default storage for it. That storage can be accessed via REST API calls using the same access token you [created](/ocr/authorization/) for Aspose.OCR Cloud API.

## Creating a folder in the storage

Folders can help you better organize files in storage.

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Files**](https://dashboard.aspose.cloud/files) page.
3. Select a storage.
4. Click **New Folder** and provide a folder name.

## Uploading a file to the storage

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Files**](https://dashboard.aspose.cloud/files) page.
3. Select a storage.
4. Navigate to the required folder.
5. Click **Upload** and select a file on your computer.

{{% alert color="primary" %}} 
If you use a third party storage (like FTP), you can upload files to it with your own tools.
{{% /alert %}}

## Protecting certain files in Aspose Cloud storage

Aspose Cloud storage (_Internal Storage_) has a file retention policy selected when it is created. You can store files in it for a maximum of 1 month; after that the old files will be automatically deleted.

To keep some files permanently:

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Storages**](https://dashboard.aspose.cloud/storages) page.
3. Click a storage.
4. Enter a file mask (regular expression) to specify the files that should be kept in the storage until they are manually deleted.

## Moving and copying files and folders within the storage

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Files**](https://dashboard.aspose.cloud/files) page.
3. Select a storage.
4. Select the required file / folder by clicking a checkbox next to it.
5. Click **Cut** to move a file / folder or click **Copy** to create a copy.
6. Navigate to the target folder and click **Paste**.

## Deleting a file or folder

{{% alert color="primary" %}} 
Deleting a folder also removes all files in it. This operation cannot be undone, unless you are using a third party storage with vendor-specific recovery mechanisms.
{{% /alert %}}

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Files**](https://dashboard.aspose.cloud/files) page.
3. Select a storage.
4. Select the required file / folder by clicking a checkbox next to it.
5. Click **Delete** and confirm the removal.

## Deleting a storage

{{% alert color="primary" %}} 
- If you are delete a third party storage, only the reference to it is actually removed from Aspose Cloud. The storage and all files in it remains intact.
- **If you delete Aspose cloud storage (_Internal storage_), it is deleted along with all files and folders!**
{{% /alert %}}

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Storages**](https://dashboard.aspose.cloud/storages) page.
3. Click a storage.
4. Click **Delete** and confirm the removal. 

## Programmatically accessing the cloud storage

Aspose.OCR Cloud provides a full-featured REST API for managing the cloud storage:

- Managing files:

    - [Uploading a file](https://apireference.aspose.cloud/ocr/#/File/UploadFile)
    - [Downloading a file](https://apireference.aspose.cloud/ocr/#/File/DownloadFile)
    - [Copying a file](https://apireference.aspose.cloud/ocr/#/File/CopyFile)
    - [Moving a file](https://apireference.aspose.cloud/ocr/#/File/MoveFile)
    - [Deleting a file](https://apireference.aspose.cloud/ocr/#/File/DeleteFile)

- Managing folders

    - [Creating a folder](https://apireference.aspose.cloud/ocr/#/Folder/CreateFolder)
    - [Getting a list of all files and subfolders](https://apireference.aspose.cloud/ocr/#/Folder/GetFilesList)
    - [Copying a folder](https://apireference.aspose.cloud/ocr/#/Folder/CopyFolder)
    - [Moving a folder](https://apireference.aspose.cloud/ocr/#/Folder/MoveFolder)
    - [Deleting a folder](https://apireference.aspose.cloud/ocr/#/Folder/DeleteFolder)

- Monitoring the storage

    - [Checking if the storage exists](https://apireference.aspose.cloud/ocr/#/Storage/StorageExists)
    - [Checking if a file or folder is available in the storage](https://apireference.aspose.cloud/ocr/#/Storage/ObjectExists)
    - [Getting the storage size used by files](https://apireference.aspose.cloud/ocr/#/Storage/GetDiscUsage)  
      _Only if supported by the storage provider._
    - [Getting all versions of a file](https://apireference.aspose.cloud/ocr/#/Storage/GetFileVersions)  
      _Only if versioning is enabled on the storage provider._

### Working with cloud storage through SDK

We provide SDKs for all popular programming languages. They wrap up all routine operations and allow you to perform all operations with the storage using simple and readable methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

- [Aspose.OCR Cloud for .NET](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet)  
- [Aspose.OCR Cloud for Java](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-java)  
- [Aspose.OCR Cloud for Python](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-python)  
- [Aspose.OCR Cloud for Node.js](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-nodejs)  
- [Aspose.OCR Cloud for Android](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-android)  
