---
title: ICorDebugController::SetAllThreadsDebugState-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugController.SetAllThreadsDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::SetAllThreadsDebugState
helpviewer_keywords:
- SetAllThreadsDebugState method [.NET Framework debugging]
- ICorDebugController::SetAllThreadsDebugState method [.NET Framework debugging]
ms.assetid: bdda4bd7-4743-4d58-a22b-8067e967db95
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8ee396c512dca2bea0a7a9737d5515defce4b2b0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugcontrollersetallthreadsdebugstate-method"></a>ICorDebugController::SetAllThreadsDebugState-Methode
Legt den Debugzustand aller verwalteten Threads im Prozess an.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT SetAllThreadsDebugState (  
    [in] CorDebugThreadState  state,  
    [in] ICorDebugThread      *pExceptThisThread  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `state`  
 [in] Der Wert der "CorDebugThreadState"-Enumeration, die den Zustand des Threads für das Debuggen angibt.  
  
 `pExceptThisThread`  
 [in] Ein Zeiger auf ein "ICorDebugThread"-Objekt, das einen Thread, der von der Debug-statuseinstellung ausgenommen werden darstellt. Wenn dieser Wert null ist, wird kein Thread befreit.  
  
## <a name="remarks"></a>Hinweise  
 Die `SetAllThreadsDebugState` Methode beeinträchtigen Threads, die nicht über sichtbar sind [EnumerateThreads-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-enumeratethreads-method.md), daher Threads, die angehalten wurden die `SetAllThreadsDebugState` Methode müssen mit fortgesetzt werden die `SetAllThreadsDebugState` Methode.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 
