---
title: ICorDebugAssemblyEnum::Next-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugAssemblyEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssemblyEnum::Next method
helpviewer_keywords:
- ICorDebugAssemblyEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugAssemblyEnum interface [.NET Framework debugging]
ms.assetid: b3e7d0c2-3baa-4ef8-8e3f-b865cf252940
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b94ae83f2fb5f71abb8cb3a5c96aac9e268fc5db
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugassemblyenumnext-method"></a>ICorDebugAssemblyEnum::Next-Methode
Ruft die angegebene Anzahl von Assemblys aus der Auflistung, beginnend mit der aktuellen Cursorposition ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugAssembly *values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `celt`  
 [in] Die Anzahl der Assemblys abgerufen werden sollen.  
  
 `values`  
 [out] Ein Array von Zeigern, von denen jedes auf ein ICorDebugAssembly-Objekt verweist, die eine Assembly darstellt.  
  
 `pceltFetched`  
 [out] Ein Zeiger auf die Anzahl der tatsächlich zurückgegebenen Assemblys. Dieser Wert kann null sein, wenn `celt` ist ein.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
