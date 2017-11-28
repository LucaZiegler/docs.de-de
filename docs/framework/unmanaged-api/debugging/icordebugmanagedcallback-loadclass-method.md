---
title: ICorDebugManagedCallback::LoadClass-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugManagedCallback.LoadClass
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugManagedCallback::LoadClass
helpviewer_keywords:
- ICorDebugManagedCallback::LoadClass method [.NET Framework debugging]
- LoadClass method [.NET Framework debugging]
ms.assetid: e58dac7b-85c3-41ca-b9aa-3a7fc9ae6680
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 3518a20567cdac8ed6587aa3dc06408ae6bf7b06
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugmanagedcallbackloadclass-method"></a><span data-ttu-id="f57a3-102">ICorDebugManagedCallback::LoadClass-Methode</span><span class="sxs-lookup"><span data-stu-id="f57a3-102">ICorDebugManagedCallback::LoadClass Method</span></span>
<span data-ttu-id="f57a3-103">Benachrichtigt den Debugger, dass eine Klasse geladen wurde.</span><span class="sxs-lookup"><span data-stu-id="f57a3-103">Notifies the debugger that a class has been loaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f57a3-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="f57a3-104">Syntax</span></span>  
  
```  
HRESULT LoadClass (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugClass     *c  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="f57a3-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="f57a3-105">Parameters</span></span>  
 `pAppDomain`  
 <span data-ttu-id="f57a3-106">[in] Ein Zeiger auf ein ICorDebugAppDomain-Objekt, das die Anwendungsdomäne darstellt, in der die Klasse geladen wurde.</span><span class="sxs-lookup"><span data-stu-id="f57a3-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain into which the class has been loaded.</span></span>  
  
 `c`  
 <span data-ttu-id="f57a3-107">[in] Ein Zeiger auf ein ICorDebugClass-Objekt, das die Klasse darstellt.</span><span class="sxs-lookup"><span data-stu-id="f57a3-107">[in] A pointer to an ICorDebugClass object that represents the class.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f57a3-108">Hinweise</span><span class="sxs-lookup"><span data-stu-id="f57a3-108">Remarks</span></span>  
 <span data-ttu-id="f57a3-109">Dieser Rückruf erfolgt nur, wenn Laden von Klassen für das Modul aktiviert wurde, die die Klasse enthält.</span><span class="sxs-lookup"><span data-stu-id="f57a3-109">This callback occurs only if class loading has been enabled for the module that contains the class.</span></span> <span data-ttu-id="f57a3-110">Laden von Klassen wird für dynamische Module immer aktiviert.</span><span class="sxs-lookup"><span data-stu-id="f57a3-110">Class loading is always enabled for dynamic modules.</span></span>  
  
 <span data-ttu-id="f57a3-111">Die `LoadClass` Rückruf stellt einen geeigneten Zeitpunkt zum Haltepunkte an neu generierte Klassen in dynamischen Modulen zu binden.</span><span class="sxs-lookup"><span data-stu-id="f57a3-111">The `LoadClass` callback provides an appropriate time to bind breakpoints to newly generated classes in dynamic modules.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f57a3-112">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="f57a3-112">Requirements</span></span>  
 <span data-ttu-id="f57a3-113">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f57a3-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f57a3-114">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f57a3-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f57a3-115">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f57a3-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f57a3-116">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f57a3-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f57a3-117">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f57a3-117">See Also</span></span>  
 [<span data-ttu-id="f57a3-118">UnloadClass-Methode</span><span class="sxs-lookup"><span data-stu-id="f57a3-118">UnloadClass Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-unloadclass-method.md)  
 [<span data-ttu-id="f57a3-119">ICorDebugManagedCallback-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="f57a3-119">ICorDebugManagedCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)