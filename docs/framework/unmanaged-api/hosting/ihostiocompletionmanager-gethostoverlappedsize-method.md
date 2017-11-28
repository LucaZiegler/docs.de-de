---
title: IHostIoCompletionManager::GetHostOverlappedSize-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostIoCompletionManager.GetHostOverlappedSize
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostIoCompletionManager::GetHostOverlappedSize
helpviewer_keywords:
- IHostIoCompletionManager::GetHostOverlappedSize method [.NET Framework hosting]
- GetHostOverlappedSize method [.NET Framework hosting]
ms.assetid: 2902578b-d5e2-4f8d-a103-0c7b6dceda9e
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 6633e0271f29d44bb1d14495d80ffdf9868485a1
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="ihostiocompletionmanagergethostoverlappedsize-method"></a><span data-ttu-id="1da35-102">IHostIoCompletionManager::GetHostOverlappedSize-Methode</span><span class="sxs-lookup"><span data-stu-id="1da35-102">IHostIoCompletionManager::GetHostOverlappedSize Method</span></span>
<span data-ttu-id="1da35-103">Ruft die Größe der benutzerdefinierten Daten, die der Host beabsichtigt, um e/a-Anforderungen angefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="1da35-103">Gets the size of any custom data the host intends to append to I/O requests.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1da35-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="1da35-104">Syntax</span></span>  
  
```  
HRESULT GetHostOverlappedSize (  
    [out] DWORD *pcbSize  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="1da35-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="1da35-105">Parameters</span></span>  
 `pcbSize`  
 <span data-ttu-id="1da35-106">[out] Ein Zeiger auf die Anzahl der Bytes, die die common Language Runtime (CLR) zusätzlich zur Größe des Win32-zuordnen soll `OVERLAPPED` Objekt.</span><span class="sxs-lookup"><span data-stu-id="1da35-106">[out] A pointer to the number of bytes that the common language runtime (CLR) should allocate in addition to the size of the Win32 `OVERLAPPED` object.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="1da35-107">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="1da35-107">Return Value</span></span>  
  
|<span data-ttu-id="1da35-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="1da35-108">HRESULT</span></span>|<span data-ttu-id="1da35-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1da35-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="1da35-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="1da35-110">S_OK</span></span>|<span data-ttu-id="1da35-111">`GetHostOverlappedSize`wurde erfolgreich zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="1da35-111">`GetHostOverlappedSize` returned successfully.</span></span>|  
|<span data-ttu-id="1da35-112">HOST_E_CLRNOTAVAILABLE ZURÜCK</span><span class="sxs-lookup"><span data-stu-id="1da35-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="1da35-113">Die CLR wurde nicht in einen Prozess geladen, oder die CLR wird in einem Zustand, in dem er nicht verwalteten Code ausführen oder den Aufruf erfolgreich verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="1da35-113">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="1da35-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="1da35-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="1da35-115">Der Aufruf ist ein Timeout aufgetreten.</span><span class="sxs-lookup"><span data-stu-id="1da35-115">The call timed out.</span></span>|  
|<span data-ttu-id="1da35-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="1da35-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="1da35-117">Der Aufrufer ist nicht Besitzer der Sperre.</span><span class="sxs-lookup"><span data-stu-id="1da35-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="1da35-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="1da35-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="1da35-119">Ein Ereignis wurde abgebrochen, während ein blockierten Thread oder eine Fiber darauf gewartet.</span><span class="sxs-lookup"><span data-stu-id="1da35-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="1da35-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="1da35-120">E_FAIL</span></span>|<span data-ttu-id="1da35-121">Ein Unbekannter Schwerwiegender Fehler aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="1da35-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="1da35-122">Wenn eine Methode E_FAIL zurückgibt, ist die CLR nicht mehr verwendbar innerhalb des Prozesses.</span><span class="sxs-lookup"><span data-stu-id="1da35-122">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="1da35-123">Nachfolgende Aufrufe zum Hosten der Methoden HOST_E_CLRNOTAVAILABLE zurück.</span><span class="sxs-lookup"><span data-stu-id="1da35-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="1da35-124">Hinweise</span><span class="sxs-lookup"><span data-stu-id="1da35-124">Remarks</span></span>  
 <span data-ttu-id="1da35-125">Alle asynchronen e/a-Aufrufe von Windows-Plattform-APIs verwenden ein Win32- `OVERLAPPED` -Objekt, das Informationen, z. B. die Position des Dateizeigers bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="1da35-125">All asynchronous I/O calls to Windows Platform APIs take a Win32 `OVERLAPPED` object, which provides information such as the file pointer position.</span></span> <span data-ttu-id="1da35-126">Um den Status beizubehalten, Anwendungen, die asynchrone e/a-Aufrufe in der Regel stellen benutzerdefinierte Daten der Struktur hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1da35-126">To maintain state, applications that make asynchronous I/O calls typically add custom data to the structure.</span></span> <span data-ttu-id="1da35-127">`GetHostOverlappedSize`und [IHostIoCompletionManager:: InitializeHostOverlapped](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-initializehostoverlapped-method.md) bieten eine Möglichkeit für den Host, diese benutzerdefinierten Daten aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="1da35-127">`GetHostOverlappedSize` and [IHostIoCompletionManager::InitializeHostOverlapped](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-initializehostoverlapped-method.md) provide an opportunity for the host to include such custom data.</span></span>  
  
 <span data-ttu-id="1da35-128">Die CLR ruft die `GetHostOverlappedSize` Methode, um die Größe der benutzerdefinierten Daten zu bestimmen, die der Host zum Anfügen an die `OVERLAPPED` Objekt.</span><span class="sxs-lookup"><span data-stu-id="1da35-128">The CLR calls the `GetHostOverlappedSize` method to determine the size of the custom data that the host intends to append to the `OVERLAPPED` object.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1da35-129">`GetHostOverlappedSize`wird nur einmal aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="1da35-129">`GetHostOverlappedSize` is called only once.</span></span> <span data-ttu-id="1da35-130">Benutzerdefinierte Daten für den Host muss die gleiche Größe für alle e/a-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="1da35-130">The host's custom data must be the same size for every I/O request.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="1da35-131">Die Größe der `OVERLAPPED` Objekt selbst ist nicht im Wert des enthalten `pcbSize`.</span><span class="sxs-lookup"><span data-stu-id="1da35-131">The size of the `OVERLAPPED` object itself is not included in the value of `pcbSize`.</span></span>  
  
 <span data-ttu-id="1da35-132">Weitere Informationen zu den `OVERLAPPED` -Struktur, finden Sie in der Dokumentation zur Windows-Plattform.</span><span class="sxs-lookup"><span data-stu-id="1da35-132">For more information about the `OVERLAPPED` structure, see the Windows Platform documentation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1da35-133">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="1da35-133">Requirements</span></span>  
 <span data-ttu-id="1da35-134">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="1da35-134">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1da35-135">**Header:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="1da35-135">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="1da35-136">**Bibliothek:** als Ressource in MSCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="1da35-136">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="1da35-137">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1da35-137">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1da35-138">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1da35-138">See Also</span></span>  
 <xref:System.Threading.NativeOverlapped>  
 [<span data-ttu-id="1da35-139">ICLRIoCompletionManager-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="1da35-139">ICLRIoCompletionManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-interface.md)  
 [<span data-ttu-id="1da35-140">IHostIoCompletionManager-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="1da35-140">IHostIoCompletionManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-interface.md)