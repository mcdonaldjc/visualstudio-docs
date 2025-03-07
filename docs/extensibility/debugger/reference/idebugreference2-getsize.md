---
description: "Gets the size, in bytes, of the value of the reference."
title: IDebugReference2::GetSize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetSize
helpviewer_keywords:
- IDebugReference2::GetSize
ms.assetid: a404ddd9-d940-4513-97cd-f52b8ab6a560
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
# IDebugReference2::GetSize

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
Gets the size, in bytes, of the value of the reference. Reserved for future use.

## Syntax

### [C#](#tab/csharp)
```csharp
int GetSize ( 
   out uint pdwSize
);
```
### [C++](#tab/cpp)
```cpp
HRESULT GetSize ( 
   DWORD* pdwSize
);
```
---

## Parameters
`pdwSize`\
[out] Returns the size, in bytes, of the value of the reference.

## Return Value
 Always returns `E_NOTIMPL`.

## See also
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
