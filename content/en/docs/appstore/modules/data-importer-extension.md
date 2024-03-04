---
title: "Data Importer"
url: /appstore/modules/data-importer/
category: "Modules"
description: "Overview of the Data Importer in Studio Pro"
tags: ["studio pro", "data importer", "excel importer"]
aliases:
    -  /appstore/modules/data-importer-extension/
---

## 1 Introduction

The [Data Importer](https://marketplace.mendix.com/link/component/219833) allows you to import data from an Excel or comma-separated value (CSV) file. You can choose which sheet and columns to import, preview the data, and create a non-persistable entity (NPE) in your domain model that corresponds to your input. You can import data into your app using the [Import Data from File](/refguide/import-data-from-file/) activity.

{{% alert color="info" %}}
The Data Importer is available in Studio Pro 10.6 and above.
{{% /alert %}}

### 1.1 Typical Use Cases

The Data Importer extension allows you to import data from Excel and CSV files directly into your app. You can create a Data Importer document to define which columns to import and an NPE to hold the imported data, along with source-to-target mapping. 

### 1.2 Features {#features}

This extension supports following source files:

* Microsoft Excel (*.xls, .xlsx, .csv*)

### 1.3 Limitations

This extension currently has the following limitations:

* The Excel column cell type is taken from the source file to determine the target attribute type; this cannot be changed during the data preview stage.
* Source data can be mapped to one entity only; associations are not currently supported 
* You cannot map the data to an already existing NPE; you have to create a new entity as part of mapping
* Enumerations are not supported 
* **String** is the default attribute type (*.csv* only)

### 1.4 Prerequisites

* Studio Pro 10.6 or above

### 1.5  Dependencies

This connector needs [Mendix Runtime](https://marketplace.mendix.com/link/component/219833) to import data from an Excel file. Download this component from the Marketplace and [add it into your app](/appstore/overview/use-content/).

## 2 Data Importer Document

### 2.1 Creating a Data Importer Document {#create-document}

To import data, right-click on the module and click **Add other** > **Data Importer**.

{{< figure src="/attachments/appstore/modules/data-importer-extension/data-importer-menu.png" >}}

Name the document, click **OK**, and the new Data Importer document opens. 

### 2.2 Previewing Data {#preview-data}

Once you have [created the Data Importer document](#create-document), click **Select a local file** to import an Excel file (*.xls* or *.xslx*) or CSV file (*.csv*).

{{< figure src="/attachments/appstore/modules/data-importer-extension/select-file-for-preview.png" >}}

#### 2.2.1 Previewing Excel Data {#preview-data-excel}

Select or drop the file in the **Select Source File** window. You can choose which sheet to import data from and specify the header row and starting data row.

* **Sheet Name** – name of the worksheet from where data needs to be imported; if the Excel has multiple worksheets, the sheet name appears in the dropdown
* **Header Row No.** – row number of the file header; the default is 1
* **Read Data From Row No.** – starting line for reading data; the default is 2

{{< figure src="/attachments/appstore/modules/data-importer-extension/select-sheet-and-header-data-row.png" >}}

Click **Preview Source Data & Entity** to view the data from the file. The first 10 rows from the source file are shown in the data preview section. The Sheet Name is used to create a NPE, but this can be edited. The column names correspond to the attribute names within the entity.

All the columns are selected (checked) by default. You can uncheck the columns you do not want to import. At the bottom of the table, you can see the target data type of the attribute, which is based on the cell type defined in the file's first data row. If any data types are incorrect, check the cell type of the first data row in Excel and adjust the cell type definition accordingly.

{{% alert color="warning" %}} Column names that do not adhere to Mendix naming conventions will be autocorrected. {{% /alert %}}

{{< figure src="/attachments/appstore/modules/data-importer-extension/preview-data-and-entity.png" >}}

#### 2.2.2 Previewing CSV Data {#preview-data-csv}

Select or drop the CSV file in the **Select Source File** window. CSV import supports multiple combinations of separator/delimiter, quote, and escape characters. It also supports importing files where the header row is absent.

Specify the values for all four configurations (Delimiter, Quote Character, Escape Character, and Add Header Row):

* **Delimiter (Separator)** – current supported delimiters are comma, semicolon, pipe, and tab; the default is comma
* **Quote Characters** – current supported quote characters are single and double quotes; the default is double quotes
* **Escape Characters** – current supported escape characters are backslash, single, and double quotes; the default is double quotes
* **Add Header Row** – specify if you want to add a header row or if the header row is already part of the CSV file; the default is the header row already included in file

Click **Preview Source Data & Entity** to view the data from the file. The first ten rows from the source file are shown in the data preview section. The file name is used to create a NPE, but this can be edited. The column names correspond to the attribute names within the entity.

All the columns are selected (checked) by default. You can uncheck the columns you do not want to import. At the bottom of the table, you can see the target data type of the attribute, which defaults to **String**.

{{% alert color="warning" %}} Column names that do not adhere to Mendix naming conventions will be autocorrected. {{% /alert %}}

For example, for the following source data (CSV), the separator is specified as Comma. The Quote and Escape Characters are set to Double Quote, and Header is included in the input file.

{{< figure src="/attachments/appstore/modules/data-importer-extension/source-csv-data.png" >}}

The data preview and resulting entity would be as seen below:

{{< figure src="/attachments/appstore/modules/data-importer-extension/preview-csv-data-and-entity.png" >}}

### 2.3 Editing an Entity {#edit-entity}

You can edit the entity in the **Entity Preview** section. The Data Importer supports various ways to:

* Edit the name of resultant entity
* Edit the name of the attribute (or attributes) of the entity
* Edit the data type of a given attribute

Click **Edit** at top-right corner of **Entity Preview**. This will render a pop-up window where you can change the name of the entity. You can also change the name of the attribute; *Original Name* is the name of the column from input file and *Attribute Name* will be the new name that you want to assign to this column. You can also change the data type of this attribute by selecting a relevant value from the drop-down as shown below.

{{< figure src="/attachments/appstore/modules/data-importer-extension/edit-csv-entity.png" >}}

Once you are satisfied with the changes, click **OK** to save or **Cancel** to discard your changes.

{{% alert color="info" %}}
The **Edit Entity** feature is useful for CSV import, as all the columns of a CSV file are marked as String by default, so you can change the data type if necessary. The following table shows the source-to-target data conversion matrix:

Input CSV File
  
| Source Type | Target- String | Target- Int | Target- Long | Target- Decimal | Target- Boolean | Target- DateTime |
| :-------- | :------- | :-------- | :------- | :-------- | :------- | :-------- |
| String  | Yes    | Partial    | Partial    | Partial    | Partial    | No    |

Input Excel File
  
| Source Type | Target- String | Target- Int | Target- Long | Target- Decimal | Target- Boolean | Target- DateTime |
| :-------- | :------- | :-------- | :------- | :-------- | :------- | :-------- |
| String  | Yes    | Partial    | Partial    | Partial    | Partial    | No    |
| Boolean  | Yes    | No    | No    | No    | Yes    | No    |
| Decimal  | Yes    | Partial    | Partial    | Yes    | No    | No    |
| DateTime  | Yes    | No    | No    | No    | No    | Yes    |

**Partial** - If source data is valid and within range, it will be converted into target data type.

{{% /alert %}}

{{% alert color="warning" %}}
* **Enum** is not supported as a target data type
* Runtime exceptions can occur if the input data cannot be converted into desired the target data type for various reasons (for example, invalid data, data truncation, casting etc.)
{{% /alert %}}

### 2.4 Creating an Entity {#create-entity}

When you are done editing the entity, click **Create Entity** > **OK**. This will create the entity in your domain model.

When the entity is created, you can view the mapping of the source columns to the target entity attributes. 

{{< figure src="/attachments/appstore/modules/data-importer-extension/source-to-target-mapping.png" >}}

The Data Importer document creation is complete and can be used to [import data in a microflow](#import-microflow).

## 3 Importing Data in a Microflow {#import-microflow}

Use the previously created Data Importer document to import data from your input file (or files) in a microflow. The example below shows how to import data from Excel file. The same steps are applicable to import data from CSV files.

1. Create a new microflow and drag the **Import data from file** activity into it.

   {{< figure src="/attachments/appstore/modules/data-importer-extension/custom-activity.png" >}}

2. Double-click the activity and in the **File** field and select an input file (either Excel or CSV).
3. In the **Data importer document** field, click **Select** and choose the Data Importer document you want to use. Choose an appropriate Data Importer document based on the input file.

   {{< figure src="/attachments/appstore/modules/data-importer-extension/choose-data-importer-template.png" >}}

4. After selecting the Data Importer document, the **Return type** and **Variable name** will autopopulate. You can also change the name of the output variable.
5. Click **OK**.

The custom activity is configured and you can import data from input files.

{{< figure src="/attachments/appstore/modules/data-importer-extension/example-microflow.png" >}}

## 4 Running Your App

To perform testing, you can do the following actions:

1. Provide a placeholder to upload a file (System.FileDocument) on a page and a button to call the configured microflow. 
2. Deploy your app locally and browse and upload an input file that resembles the file used to create Data Importer document.
3. View the message about x number of rows being imported into a list of entities. 

{{< figure src="/attachments/appstore/modules/data-importer-extension/local-app-run.png" >}}

## 5 Known Issues

### 5.1 Unchecked Columns

It is not possible to rename an attribute or change a data type if there are unchecked columns. To avoid this issue, format your Excel or CSV file in a way that does not require you to uncheck any columns after inputting to Studio Pro.