---
description: "Describes an array of unique identifiers for available debug engines."
title: GUID_ARRAY | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GUID_ARRAY structure
ms.assetid: 9e12500c-2c1c-49b1-a0ba-e08366c97eb8
author: maiak
ms.author: maiak
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
---
# GUID_ARRAY

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
Describes an array of unique identifiers for available debug engines.

## Syntax

### [C#](#tab/csharp)
```csharp
public struct GUID_ARRAY
{
    public uint dwCount;
    public Guid Members;
}
```
### [C++](#tab/cpp)
```cpp
typedef struct tagGUID_ARRAY
{
    DWORD dwCount;
    GUID *Members;
} GUID_ARRAY;
```
---

## Members
`dwCount`\
Number of unique identifiers in the array.

`Members`\
Array that contains unique identifiers.

## Remarks
This structure is returned by the [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md) method.

## Requirements
Header: Msdbg.h

Namespace: Microsoft.VisualStudio.Debugger.Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## See also
- [Structures and Unions](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)
