---
title: "How to: Programmatically create new Visio documents"
description: Learn how you can programmatically create a new Microsoft Visio drawing document and add it to the Documents collection of open Visio documents.
ms.date: "02/02/2017"
ms.topic: "how-to"
dev_langs:
  - "VB"
  - "CSharp"
helpviewer_keywords:
  - "Visio [Office development in Visual Studio], creating Visio documents"
  - "documents [Office development in Visual Studio], creating Visio documents"
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
  - "office"
---
# How to: Programmatically create new Visio documents

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
  When you create a new Microsoft Office Visio drawing document, you add it to the `Microsoft.Office.Interop.Visio.Documents` collection of open Visio documents. Consequently, the `Microsoft.Office.Interop.Visio.Documents.Add` method creates a new Visio drawing document. For more information, see the VBA reference documentation for the [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) method.

## Create new blank documents

### To create a new document

- Use the `Microsoft.Office.Interop.Visio.Documents.Add` method to create a new blank document that is not based on a template.

     ### [C#](#tab/csharp)
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet1":::

     ### [VB](#tab/vb)
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet1":::
     ---

## Create documents copied from existing documents
 The `Microsoft.Office.Interop.Visio.Documents.Add` method can create a new document that is a copy of an existing Visio document. You must supply the file name and fully qualified path of the diagram.

### To create a new document that is copied from an existing document

- Call the `Microsoft.Office.Interop.Visio.Documents.Add` method and specify the path of the Visio diagram.

    ### [C#](#tab/csharp)
    :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet2":::

    ### [VB](#tab/vb)
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet2":::
    ---

## Create stencils copied from existing stencils
 The [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) method can create a new stencil that is a copy of an existing Visio stencil. You must supply the file name and fully qualified path of the stencil.

### To create a new stencil that is copied from an existing stencil

- Call the `Microsoft.Office.Interop.Visio.Documents.Add` method and specify the path of the stencil.

     ### [C#](#tab/csharp)
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet3":::

     ### [VB](#tab/vb)
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet3":::
     ---

## Create documents based on existing templates
 The `Microsoft.Office.Interop.Visio.Documents.Add` method can create a new document (a *.vsd* file) that is based on an existing Visio template (a *.vst* file). This method copies the stencils, styles, and settings that are part of the template workspace. You must supply the file name and fully qualified path of the template.

### To create a new document that is based on an existing template

- Call the `Microsoft.Office.Interop.Visio.Documents.Add` method and specify the path of the template.

     ### [C#](#tab/csharp)
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet4":::

     ### [VB](#tab/vb)
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet4":::
     ---

## Compile the code
 This code example requires the following:

- A Visio document named `myDrawing.vsd` must be located in a directory named `Test` in the *My Documents* folder (for Windows XP and earlier) or the *Documents* folder (for Windows Vista).

- A Visio document named `myStencil.vss` must be located in a directory named `Test` in the *My Documents* folder (for Windows XP and earlier) or the *Documents* folder (for Windows Vista).

- A Visio document named `myTemplate.vst` must be located in a directory named `Test` in the *My Documents* folder (for Windows XP and earlier) or the *Documents* folder (for Windows Vista).

## See also
- [Visio solutions](../vsto/visio-solutions.md)
- [Visio object model overview](../vsto/visio-object-model-overview.md)
- [How to: Programmatically open Visio documents](../vsto/how-to-programmatically-open-visio-documents.md)
- [How to: Programmatically close Visio documents](../vsto/how-to-programmatically-close-visio-documents.md)
- [How to: Programmatically save Visio documents](../vsto/how-to-programmatically-save-visio-documents.md)
- [How to: Programmatically print Visio documents](../vsto/how-to-programmatically-print-visio-documents.md)
