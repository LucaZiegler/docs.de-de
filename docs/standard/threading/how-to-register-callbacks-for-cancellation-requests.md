---
title: "Gewusst wie: Registrieren von Rückrufen für Abbruchanforderungen"
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
- cancellation, how to register callbacks
ms.assetid: 8838dd75-18ed-4b8b-b322-cd4531faac64
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: b71ebee3a28fb6a829edf657f56e54799097f351
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="how-to-register-callbacks-for-cancellation-requests"></a>Gewusst wie: Registrieren von Rückrufen für Abbruchanforderungen
Im folgenden Beispiel wird gezeigt, wie Sie einen Delegaten registrieren, der aufgerufen wird, wenn eine <xref:System.Threading.CancellationToken.IsCancellationRequested%2A>-Eigenschaft aufgrund eines Aufrufs von <xref:System.Threading.CancellationTokenSource.Cancel%2A> für das Objekt, das das Token erstellt hat, den Wert „true“ aufweist. Verwenden Sie dieses Verfahren zum Abbrechen asynchroner Vorgänge, die das einheitliche Abbruchframework nicht systemeigen unterstützen, und für das Aufheben der Sperre von Methoden, die möglicherweise auf den Abschluss eines asynchronen Vorgangs warten.  
  
> [!NOTE]
>  Wenn "Nur eigenen Code" aktiviert ist, unterbricht Visual Studio die Ausführung in einigen Fällen in der Zeile, die die Ausnahme auslöst, und eine Fehlermeldung zu einer nicht vom Benutzercode behandelten Ausnahme wird angezeigt. Dieser Fehler hat keine Auswirkungen. Sie können F5 drücken, um den Vorgang fortzusetzen. In diesem Fall wird das in den nachstehenden Beispielen veranschaulichte Ausnahmebehandlungsverhalten angewendet. Um zu verhindern, dass Visual Studio die Ausführung beim ersten Fehler unterbricht, deaktivieren Sie unter **Extras, Optionen, Debugging, Allgemein** das Kontrollkästchen „Nur eigenen Code“.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die <xref:System.Net.WebClient.CancelAsync%2A>-Methode als aufzurufende Methode registriert, wenn durch das Abbruchtoken der Abbruch angefordert wird.  
  
 [!code-csharp[Conceptual.Cancellation.Callback#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.cancellation.callback/cs/howtoexample1.cs#1)]
 [!code-vb[Conceptual.Cancellation.Callback#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.cancellation.callback/vb/howtoexample1.vb#1)]  
  
 Wenn der Abbruch zum Zeitpunkt der Rückrufregistrierung bereits angefordert wurde, wird der Rückruf trotzdem garantiert aufgerufen. In diesem speziellen Fall bleibt die <xref:System.Net.WebClient.CancelAsync%2A>-Methode wirkungslos, wenn kein asynchroner Vorgang ausgeführt wird. Das Aufrufen der Methode ist daher immer sicher.  
  
## <a name="see-also"></a>Siehe auch  
 [Abbruch in verwalteten Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)
