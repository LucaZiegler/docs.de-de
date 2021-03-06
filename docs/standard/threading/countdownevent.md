---
title: CountdownEvent
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- synchronization primitives, CountdownEvent
ms.assetid: eec3812a-e20f-4ecd-bfef-6921d508b708
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 144bcde6c4c8fb227773fe613da8445f100ce66d
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="countdownevent"></a>CountdownEvent
<xref:System.Threading.CountdownEvent?displayProperty=nameWithType> ist eine Synchronisierungsprimitive, die die Blockierung ihrer wartenden Threads nach einer bestimmten Zahl an sie gerichteter Signalisierungen aufhebt. <xref:System.Threading.CountdownEvent> eignet sich für Szenarien, in denen Sie andernfalls ein <xref:System.Threading.ManualResetEvent> oder <xref:System.Threading.ManualResetEventSlim> verwenden und manuell eine Variable vor dem Signalisieren des Ereignisses verringern müssen. In einem Fork/Join-Szenario können Sie z.B. nur ein <xref:System.Threading.CountdownEvent> mit einer Signalanzahl von 5 erstellen und dann fünf Arbeitselemente im Threadpool starten und jedes Arbeitselement bei Abschluss <xref:System.Threading.CountdownEvent.Signal%2A> aufrufen lassen. Jeder Aufruf von <xref:System.Threading.CountdownEvent.Signal%2A> reduziert die Signalanzahl um 1. Im Hauptthread wird der Aufruf von <xref:System.Threading.CountdownEvent.Wait%2A> blockiert, bis die Signalanzahl 0 (null) ist.  
  
> [!NOTE]
>  Erwägen Sie für Code, der nicht für die Interaktion mit älteren .NET Framework-Synchronisierungs-APIs vorgesehen ist, einen noch einfacheren Ansatz zum Ausdrücken der Fork/Join-Parallelität mit Verwendung von <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>-Objekten oder der <xref:System.Threading.Tasks.Parallel.Invoke%2A>-Methode.  
  
 <xref:System.Threading.CountdownEvent> besitzt diese zusätzlichen Features:  
  
-   Der Wait-Vorgang kann mithilfe von Abbruchtoken abgebrochen werden.  
  
-   Die Signalanzahl kann nach dem Erstellen der Instanz erhöht werden.  
  
-   Instanzen können wiederverwendet werden, nachdem <xref:System.Threading.CountdownEvent.Wait%2A> zur Rückgabe die <xref:System.Threading.CountdownEvent.Reset%2A>-Methode aufgerufen hat.  
  
-   Instanzen machen ein <xref:System.Threading.WaitHandle> für die Integration mit anderen .NET Framework-Synchronisierungs-APIs wie <xref:System.Threading.WaitHandle.WaitAll%2A> verfügbar.  
  
## <a name="basic-usage"></a>Grundlegende Verwendung  
 Im folgenden Beispiel wird die Verwendung eines <xref:System.Threading.CountdownEvent> mit <xref:System.Threading.ThreadPool>-Arbeitselementen veranschaulicht.  
  
 [!code-csharp[CDS_CountdownEvent#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#01)]
 [!code-vb[CDS_CountdownEvent#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/module1.vb#01)]  
  
## <a name="countdownevent-with-cancellation"></a>CountdownEvent mit Abbruch  
 Im folgenden Beispiel wird der Abbruch des Wartevorgangs für <xref:System.Threading.CountdownEvent> durch Verwenden eines Abbruchtokens beschrieben. Das grundlegende Muster folgt dem in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] eingeführten Modell für einheitlichen Abbruch. Weitere Informationen finden Sie unter [Abbruch in verwalteten Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md).  
  
 [!code-csharp[CDS_CountdownEvent#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#02)]
 [!code-vb[CDS_CountdownEvent#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/canceleventwait.vb#02)]  
  
 Beachten Sie, dass der Wartevorgang nicht die Threads abbricht, die ihn signalisieren. In der Regel wird der Abbruch auf eine logische Operation angewendet, und das kann sowohl das Warten auf das Ereignis als auch alle Arbeitselemente beinhalten, die der Wartevorgang synchronisiert. In diesem Beispiel wird jedem Arbeitselement eine Kopie desselben Abbruchtokens übergeben, sodass es auf die Abbruchanforderung reagieren kann.  
  
## <a name="see-also"></a>Siehe auch  
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)
