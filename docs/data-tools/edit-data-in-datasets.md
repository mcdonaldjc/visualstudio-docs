---
title: Edit data in datasets
description: Learn to edit data in datasets. Know how to edit dataset rows, insert new rows into a dataset, determine if there are changed rows, and locate rows with errors.
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
---
# Edit data in datasets

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
You edit data in data tables much like you edit the data in a table in any database. The process can include inserting, updating, and deleting records in the table. In a data-bound form, you can specify which fields are user-editable. In those cases, the data-binding infrastructure handles all the change tracking so that the changes can be sent back to the database later. If you programmatically make edits to data, and you intend to send those changes back to the database, you must use the objects and methods that do the change tracking for you.

In addition to changing the actual data, you can also query a <xref:System.Data.DataTable> to return specific rows of data. For example, you might query for individual rows, specific versions of rows (original and proposed), rows that have changed, or rows that have errors.

## To edit rows in a dataset
To edit an existing row in a <xref:System.Data.DataTable>, you need to locate the <xref:System.Data.DataRow> you want to edit, and then assign the updated values to the desired columns.

If you don't know the index of the row you want to edit, use the `FindBy` method to search by the primary key:

### [C#](#tab/csharp)
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet3":::

### [VB](#tab/vb)
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet3":::
---

If you know the row index, you can access and edits rows as follows:

### [C#](#tab/csharp)
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet5":::

### [VB](#tab/vb)
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet5":::
---

## To insert new rows into a dataset
Applications that use data-bound controls typically add new records through the **Add New** button on a [BindingNavigator control](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms).

To manually add new records to a dataset, create a new data row by calling the method on the DataTable. Then, add the row to the <xref:System.Data.DataRow> collection (<xref:System.Data.DataTable.Rows%2A>) of the <xref:System.Data.DataTable>:

### [C#](#tab/csharp)
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet1":::

### [VB](#tab/vb)
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet1":::
---

In order to retain the information that the dataset needs to send updates to the data source, use the <xref:System.Data.DataRow.Delete%2A> method to remove rows in a data table. For example, if your application uses a TableAdapter (or <xref:System.Data.Common.DataAdapter>), the TableAdapter's `Update` method deletes rows in the database that have a <xref:System.Data.DataRow.RowState%2A> of <xref:System.Data.DataRowState.Deleted>.

If your application does not need to send updates back to a data source, it's possible to remove records by directly accessing the data row collection (<xref:System.Data.DataRowCollection.Remove%2A>).

#### To delete records from a data table

- Call the <xref:System.Data.DataRow.Delete%2A> method of a <xref:System.Data.DataRow>.

     This method doesn't physically remove the record. Instead, it marks the record for deletion.

    > [!NOTE]
    > If you get the count property of a <xref:System.Data.DataRowCollection>, the resulting count includes records that have been marked for deletion. To get an accurate count of records that aren't marked for deletion, you can loop through the collection looking at the <xref:System.Data.DataRow.RowState%2A> property of each record. (Records marked for deletion have a <xref:System.Data.DataRow.RowState%2A> of <xref:System.Data.DataRowState.Deleted>.) Alternatively, you can create a data view of a dataset that filters based on row state and get the count property from there.

The following example shows how to call the <xref:System.Data.DataRow.Delete%2A> method to mark the first row in the `Customers` table as deleted:

### [C#](#tab/csharp)
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet8":::

### [VB](#tab/vb)
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet8":::
---

## Determine if there are changed rows
When changes are made to records in a dataset, information about those changes is stored until you commit them. You commit the changes when you call the `AcceptChanges` method of a dataset or data table, or when you call the `Update` method of a TableAdapter or data adapter.

Changes are tracked two ways in each data row:

- Each data row contains information related to its <xref:System.Data.DataRow.RowState%2A> (for example, <xref:System.Data.DataRowState.Added>, <xref:System.Data.DataRowState.Modified>, <xref:System.Data.DataRowState.Deleted>, or <xref:System.Data.DataRowState.Unchanged>).

- Each changed data row contains multiple versions of that row (<xref:System.Data.DataRowVersion>), the original version (before changes) and the current version (after changes). During the period when a change is pending (the time when you can respond to the <xref:System.Data.DataTable.RowChanging> event), a third version — the proposed version— is available as well.

The <xref:System.Data.DataSet.HasChanges%2A> method of a dataset returns `true` if changes have been made in the dataset. After determining that changed rows exist, you can call the `GetChanges` method of a <xref:System.Data.DataSet> or <xref:System.Data.DataTable> to return a set of changed rows.

#### To determine if changes have been made to any rows

- Call the <xref:System.Data.DataSet.HasChanges%2A> method of a dataset to check for changed rows.

The following example shows how to check the return value from the <xref:System.Data.DataSet.HasChanges%2A> method to detect whether there are any changed rows in a dataset named `NorthwindDataset1`:

### [C#](#tab/csharp)
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet12":::

### [VB](#tab/vb)
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet12":::
---

## Determine the type of changes
You can also check to see what type of changes were made in a dataset by passing a value from the <xref:System.Data.DataRowState> enumeration to the <xref:System.Data.DataSet.HasChanges%2A> method.

#### To determine what type of changes have been made to a row

- Pass a <xref:System.Data.DataRowState> value to the <xref:System.Data.DataSet.HasChanges%2A> method.

The following example shows how to check a dataset named `NorthwindDataset1` to determine if any new rows have been added to it:

### [C#](#tab/csharp)
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet13":::

### [VB](#tab/vb)
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet13":::
---

## To locate rows that have errors
When working with individual columns and rows of data, you might encounter errors. You can check the `HasErrors` property to determine if errors exist in a <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, or <xref:System.Data.DataRow>.

1. Check the `HasErrors` property to see if there are any errors in the dataset.

2. If the `HasErrors` property is `true`, iterate through the collections of tables, and then the through the rows, to find the row with the error.

### [C#](#tab/csharp)
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet23":::

### [VB](#tab/vb)
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet23":::
---

## See also

- [Dataset tools in Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
