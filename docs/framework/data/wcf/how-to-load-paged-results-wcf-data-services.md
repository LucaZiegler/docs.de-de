---
title: 'Gewusst wie: Laden von ausgelagerten Ergebnissen (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, deferred content
- WCF Data Services, loading data
ms.assetid: bb786ea4-f3ef-4ad3-9a41-3a0b7feb6a1f
ms.openlocfilehash: 6706ad2eb6821c2c30b5d2482f709ba849b59f32
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-load-paged-results-wcf-data-services"></a>Gewusst wie: Laden von ausgelagerten Ergebnissen (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] ermöglicht es dem Datendienst, die Anzahl von Entitäten zu beschränken, die in einem einzelnen Antwortfeed zurückgegeben werden. In diesem Fall enthält der abschließende Eintrag im Feed einen Link zur nächsten Datenseite. Der URI zur nächsten Datenseite wird abgerufen, indem Sie die <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A>-Methode der <xref:System.Data.Services.Client.QueryOperationResponse%601> aufrufen, die beim Ausführen der <xref:System.Data.Services.Client.DataServiceQuery%601> zurückgegeben wird. Der von diesem Objekt dargestellte URI wird dann verwendet, um die nächste Ergebnisseite zu laden. Weitere Informationen finden Sie unter [Content verzögerte Laden von](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md).  
  
 Im Beispiel in diesem Thema werden der Northwind-Beispieldatendienst und automatisch generierte Client-Datendienstklassen verwendet. Dieser Dienst und die clientdatenklassen werden erstellt, wenn Sie die [WCF Data Services-Schnellstart](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel werden `do…while`-Entitäten aus ausgelagerten Ergebnissen aus dem Datendienst mithilfe einer `Customers`-Schleife geladen.  
  
 [!code-csharp[Astoria Northwind Client#GetCustomersPaged](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getcustomerspaged)]
 [!code-vb[Astoria Northwind Client#GetCustomersPaged](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getcustomerspaged)]  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel werden verknüpfte `Orders`-Entitäten mit jeder `Customers`-Entität zurückgegeben, und es wird eine `do…while`-Schleife zum Laden von `Customers`-Entitätenseiten und eine geschachtelte `while`-Schleife zum Laden verknüpfter `Orders`-Entitäten aus dem Datendienst verwendet.  
  
 [!code-csharp[Astoria Northwind Client#GetCustomersPagedNested](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getcustomerspagednested)]
 [!code-vb[Astoria Northwind Client#GetCustomersPagedNested](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getcustomerspagednested)]  
  
## <a name="see-also"></a>Siehe auch  
 [Laden von verzögerten Inhalten](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)  
 [Vorgehensweise: Laden von verbundenen Entitäten](../../../../docs/framework/data/wcf/how-to-load-related-entities-wcf-data-services.md)
