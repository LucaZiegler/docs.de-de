---
title: 'Gewusst wie: Filtern auf DataContext-Ebene'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 15505cd7-0df2-427a-9f86-e0f96f60ee2e
ms.openlocfilehash: c04be0bb955cff4bf796d14d45b39cac7ce4352d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-filter-at-the-datacontext-level"></a>Gewusst wie: Filtern auf DataContext-Ebene
Sie können `EntitySets` auf `DataContext`-Ebene filtern. Solche Filter gelten für alle Abfragen, die mit dieser <xref:System.Data.Linq.DataContext>-Instanz erstellt wurden.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird <xref:System.Data.Linq.DataLoadOptions.AssociateWith%28System.Linq.Expressions.LambdaExpression%29?displayProperty=nameWithType> verwendet, um die vorab geladenen Reihenfolgen für Kunden nach `ShippedDate` zu filtern.  
  
 [!code-csharp[DLinqQueryConcepts#10](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#10)]
 [!code-vb[DLinqQueryConcepts#10](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#10)]  
  
## <a name="see-also"></a>Siehe auch  
 [Abfragekonzepte](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)
