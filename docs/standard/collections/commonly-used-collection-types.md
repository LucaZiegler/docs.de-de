---
title: Häufig verwendete Auflistungstypen
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology: dotnet-standard
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- collections [.NET Framework], generic
- objects [.NET Framework], grouping in collections
- generics [.NET Framework], collections
- IList interface, grouping data in collections
- IDictionary interface, grouping data in collections
- grouping data in collections, generic collection types
- Collections classes
- generic collections
ms.assetid: f5d4c6a4-0d7b-4944-a9fb-3b12d9ebfd55
caps.latest.revision: 29
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 127813e52b6e72f896ebe4f5017651467f748a04
ms.sourcegitcommit: 2e8acae16ae802f2d6d04e3ce0a6dbf04e476513
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="commonly-used-collection-types"></a>Häufig verwendete Auflistungstypen
Auflistungstypen sind die allgemeinen Variationen von Datenauflistungen, z. B. Hashtabellen, Warteschlangen, Stapel, Sammlungen, Wörterbücher und Listen.  
  
 Auflistungen basieren auf der <xref:System.Collections.ICollection>-Schnittstelle, der <xref:System.Collections.IList>-Schnittstelle, der <xref:System.Collections.IDictionary>-Schnittstelle oder auf ihren generischen Entsprechungen. Die <xref:System.Collections.IList>-Schnittstelle und die <xref:System.Collections.IDictionary>-Schnittstelle leiten sich beide aus der <xref:System.Collections.ICollection>-Schnittstelle ab. Daher basieren alle Auflistungen direkt oder indirekt auf der <xref:System.Collections.ICollection>-Schnittstelle. In Auflistungen, die auf der <xref:System.Collections.IList>-Schnittstelle basieren (zum Beispiel <xref:System.Array>, <xref:System.Collections.ArrayList> oder <xref:System.Collections.Generic.List%601>) oder direkt auf der <xref:System.Collections.ICollection>-Schnittstelle (zum Beispiel <xref:System.Collections.Queue>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, <xref:System.Collections.Stack>, <xref:System.Collections.Concurrent.ConcurrentStack%601> oder <xref:System.Collections.Generic.LinkedList%601>), enthält jedes Element nur einen Wert. In Auflistungen, die auf der <xref:System.Collections.IDictionary>-Schnittstelle basieren (zum Beispiel die Klassen <xref:System.Collections.Hashtable> und <xref:System.Collections.SortedList>, die generischen Klassen <xref:System.Collections.Generic.Dictionary%602> und <xref:System.Collections.Generic.SortedList%602>), oder die auf den <xref:System.Collections.Concurrent.ConcurrentDictionary%602>-Klassen basieren, enthält jedes Element einen Schlüssel und einen Wert.  Die <xref:System.Collections.ObjectModel.KeyedCollection%602>-Klasse ist eindeutig, da sie eine Liste von Werten mit Schlüsseln darstellt, die in den Werten eingebettet sind. Deshalb verhält sie sich wie eine Liste und wie ein Wörterbuch.  
  
 Generische Auflistungen sind die beste Lösung für eine starke Typisierung. Wenn Ihre Sprache allerdings keine generischen Auflistungen unterstützt, enthält der <xref:System.Collections>-Namespace Basisauflistungen, zum Beispiel <xref:System.Collections.CollectionBase>, <xref:System.Collections.ReadOnlyCollectionBase> und <xref:System.Collections.DictionaryBase>. Dabei handelt es sich um abstrakte Basisklassen, die erweitert werden können, um Auflistungsklassen zu erstellen, die stark typisiert sind. Beim effizienter Zugriff auf Multithreadauflistungen erforderlich ist, verwenden Sie die generischen Auflistungen im <xref:System.Collections.Concurrent>-Namespace.  
  
 Auflistungen können variieren, je nachdem, wie die Elemente gespeichert werden, wie sie sortiert werden, wie Suchvorgänge ausgeführt werden und wie Vergleiche vorgenommen werden. Die <xref:System.Collections.Queue>-Klasse und die generische <xref:System.Collections.Generic.Queue%601>-Klasse stellen First-in-First-Out-Listen bereit, während die <xref:System.Collections.Stack>-Klasse und die generische <xref:System.Collections.Generic.Stack%601>-Klasse Last-in-First-Out-Listen bereitstellen. Die <xref:System.Collections.SortedList>-Klasse und die generische <xref:System.Collections.Generic.SortedList%602>-Klasse stellen sortierte Versionen der <xref:System.Collections.Hashtable>-Klasse und der generischen <xref:System.Collections.Generic.Dictionary%602>-Klasse bereit. Der Zugriff auf die Elemente einer <xref:System.Collections.Hashtable> oder <xref:System.Collections.Generic.Dictionary%602> ist nur über den Schlüssel des Elements möglich, aber der Zugriff auf Elemente einer <xref:System.Collections.SortedList> oder <xref:System.Collections.ObjectModel.KeyedCollection%602> ist über den Schlüssel oder den Index des Elements möglich. Die Indizes in allen Auflistungen sind nullbasiert, mit Ausnahme von <xref:System.Array>, wodurch auch Arrays, die nicht nullbasiert sind, zulässig sind.  
  
 Mit der LINQ to Objects-Funktion können Sie LINQ-Abfragen für den Zugriff auf Objekte im Arbeitsspeicher verwenden, solange der Objekttyp <xref:System.Collections.IEnumerable> oder <xref:System.Collections.Generic.IEnumerable%601> implementiert. LINQ-Abfragen bieten ein allgemeines Muster für den Datenzugriff, sind normalerweise präziser und besser lesbar als standardmäßige `foreach`-Schleifen und stellen Filter-, Sortier- und Gruppierungsfunktionen bereit. LINQ-Abfragen können auch die Leistung verbessern. Weitere Informationen finden Sie unter [LINQ-zu-Objekte](https://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9) und [Parallel LINQ (PLINQ) (Paralleles LINQ (PLINQ))](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## <a name="related-topics"></a>Verwandte Themen  
  
|Titel|description|  
|-----------|-----------------|  
|[Auflistungen und Datenstrukturen](../../../docs/standard/collections/index.md)|Erläutert die unterschiedlichen Auflistungstypen, die in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] verfügbar sind, z. B. Stapel, Warteschlangen, Listen, Arrays und Wörterbücher.|  
|[Hashtable-Auflistungstyp und Dictionary-Auflistungstyp](../../../docs/standard/collections/hashtable-and-dictionary-collection-types.md)|Beschreibt die Funktionen von generischen und nicht generischen hashbasierten Wörterbuchtypen.|  
|[Sortierte Auflistungstypen](../../../docs/standard/collections/sorted-collection-types.md)|Beschreibt Klassen, die Sortierfunktionen für Listen und Sätze bereitstellen.|  
|[Generika](../../../docs/standard/generics/index.md)|Beschreibt das Generikafeature, einschließlich der generischen Auflistungen, Delegaten und Schnittstellen, die von [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] bereitgestellt werden. Enthält Links zur Featuredokumentation für C#, Visual Basic und Visual C++ sowie zu unterstützenden Technologien wie der Reflektion.|  
  
## <a name="reference"></a>Referenz  
 <xref:System.Collections?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic?displayProperty=nameWithType>  
  
 <xref:System.Collections.ICollection?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic.ICollection%601?displayProperty=nameWithType>  
  
 <xref:System.Collections.IList?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic.IList%601?displayProperty=nameWithType>  
  
 <xref:System.Collections.IDictionary?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=nameWithType>
