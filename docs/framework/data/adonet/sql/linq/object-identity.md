---
title: "Objektidentit&#228;t | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c788f2f9-65cc-4455-9907-e8388a268e00
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Objektidentit&#228;t
Objekte verfügen zur Laufzeit über eindeutige Identitäten.  Zwei Variablen, die sich auf das gleiche Objekt beziehen, verweisen tatsächlich auf die gleiche Objektinstanz.  Aufgrund dieser Tatsache sind Änderungen, die Sie über einen Pfad durch eine Variable vornehmen, sofort über die andere Variable sichtbar.  
  
 Zeilen in einer relationalen Datenbanktabelle weisen keine eindeutigen Identitäten auf.  Da jede Zeile über einen eindeutigen Primärschlüssel verfügt, weisen keine zwei Zeilen den gleichen Schlüsselwert auf.  Diese Tatsache schränkt jedoch nur den Inhalt der Datenbanktabelle ein.  
  
 Tatsächlich werden die Daten in der Regel aus der Datenbank in eine andere Kategorie abgerufen, von der aus sie durch eine Anwendung genutzt werden.  Dies ist das von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] unterstützte Modell.  Wenn Daten in Form von Zeilen aus der Datenbank abgerufen werden, können Sie nicht davon ausgehen, dass zwei Zeilen, die die gleichen Daten darstellen, tatsächlich der gleichen Zeileninstanz entsprechen.  Wenn Sie einen bestimmten Kunden zweimal abrufen, erhalten Sie zwei Datenzeilen. Jede Zeile enthält die gleichen Informationen.  
  
 Von Objekten erwarten Sie etwas ganz anderes.  Sie gehen davon aus, dass Sie bei wiederholtem Abrufen der gleichen Informationen aus dem <xref:System.Data.Linq.DataContext> tatsächlich die gleiche Objektinstanz erhalten.  Sie erwarten dieses Verhalten, da Objekte für Ihre Anwendung von besonderer Bedeutung sind und weil Sie von einem objektgemäßen Verhalten ausgehen.  Sie haben sie als Hierarchien oder Graphen entworfen.  Sie möchten diese Objekte als solche abrufen und keine mehrfach replizierten Instanzen erhalten, nur weil Sie die gleichen Informationen mehrfach abrufen.  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] verwaltet der <xref:System.Data.Linq.DataContext> die Objektidentität.  Wenn Sie eine neue Zeile aus der Datenbank abrufen, wird diese mit ihrem Primärschlüssel in einer Identitätstabelle protokolliert, und es wird ein neues Objekt erstellt.  Jedes Mal, wenn Sie die gleiche Zeile abrufen, wird die ursprüngliche Objektinstanz an die Anwendung zurückgegeben.  Auf diese Weise übersetzt der <xref:System.Data.Linq.DataContext> das Identitätskonzept aus Sicht der Datenbank \(Primärschlüssel\) in das Identitätskonzept aus Sicht der Sprache \(Instanzen\).  Die Anwendung sieht nur das Objekt in dem Zustand, in dem es zuerst abgerufen wurde.  Die neuen Daten werden \(sofern sie abweichen\) verworfen.  Weitere Informationen finden Sie unter [Abrufen von Objekten aus dem Identitäts\-Cache](../../../../../../docs/framework/data/adonet/sql/linq/retrieving-objects-from-the-identity-cache.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] verwendet diesen Ansatz zur Verwaltung der Integrität lokaler Objekte, um vollständige Updates zu unterstützen.  Da die einzigen Änderungen, die nach dem ersten Erstellen des Objekts auftreten, von der Anwendung vorgenommen werden, ist die Absicht der Anwendung klar.  Sind zwischenzeitlich Änderungen durch eine externe Partei erfolgt, werden diese zum Zeitpunkt des Aufrufs von `SubmitChanges()` identifiziert.  
  
> [!NOTE]
>  Lässt sich das von der Abfrage angeforderte Objekt leicht als bereits abgerufen identifizieren, wird keine Abfrage ausgeführt.  Die Identitätstabelle dient als Cache für alle zuvor abgerufenen Objekte.  
  
## Beispiele  
  
### Objektzwischenspeicherung, Beispiel 1  
 Wenn Sie in diesem Beispiel eine Abfrage zweimal ausführen, erhalten Sie stets einen Verweis auf das gleiche Objekt im Arbeitsspeicher.  
  
 [!code-csharp[DLinqObjectIdentity#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#1)]
 [!code-vb[DLinqObjectIdentity#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#1)]  
  
### Objektzwischenspeicherung, Beispiel 2  
 Wenn Sie in diesem Beispiel unterschiedliche Abfragen ausführen, die die gleiche Zeile aus der Datenbank zurückgeben, erhalten Sie stets einen Verweis auf das gleiche Objekt im Arbeitsspeicher.  
  
 [!code-csharp[DLinqObjectIdentity#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#2)]
 [!code-vb[DLinqObjectIdentity#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#2)]  
  
## Siehe auch  
 [Hintergrundinformationen](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)