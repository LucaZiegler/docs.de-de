---
title: ICorDebugBreakpoint Schnittstelle1
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpoint
helpviewer_keywords:
- ICorDebugBreakpoint interface [.NET Framework debugging]
ms.assetid: aa5ad3d7-e1bb-42af-99bc-471224e3bcaa
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 220cd1a41ed69325b557e6498a511865b78817ec
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugbreakpoint-interface1"></a>ICorDebugBreakpoint Schnittstelle1
Stellt einen Haltepunkt in einer Funktion oder einen Beobachtungspunkt für einen Wert dar.  
  
## <a name="methods"></a>Methoden  
  
|Methode|Beschreibung|  
|------------|-----------------|  
|[Activate-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugbreakpoint-activate-method.md)|Legt den Zustand "aktiven" dieses `ICorDebugBreakpoint`.|  
|[IsActive-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugbreakpoint-isactive-method.md)|Ruft einen Wert, der angibt, ob dies `ICorDebugBreakpoint` aktiv ist.|  
  
## <a name="remarks"></a>Hinweise  
 Bedingte Ausdrücke unterstützt Haltepunkte nicht direkt. Wenn solche Funktionen gewünscht ist, muss ein Debugger implementieren sie auf der Basis von `ICorDebugBreakpoint`.  
  
 ICorDebugFunctionBreakpoint-Schnittstelle erweitert `ICorDebugBreakpoint` um Haltepunkte innerhalb von Funktionen zu unterstützen.  
  
> [!NOTE]
>  Diese Schnittstelle kann weder computerübergreifend noch prozessübergreifend remote aufgerufen werden.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Debuggen von Schnittstellen](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
