---
title: Benutzerdefinierte CLR-Typen
ms.date: 03/30/2017
ms.assetid: 9f70e0b0-3a0d-4eb1-b914-07a5d0c167c2
ms.openlocfilehash: 344245ea7c67d7b5363c17bb42e2606ca11142bf
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="clr-user-defined-types"></a>Benutzerdefinierte CLR-Typen
Microsoft SQL Server bietet Unterstützung für benutzerdefinierte Typen (User-Defined Types, UDTs), die mit der CLR (Common Language Runtime) von Microsoft .NET Framework implementiert werden. Durch die Integration der CLR in SQL Server verfügen Sie über einen Mechanismus, mit dessen Hilfe Sie das Typsystem der Datenbank erweitern können. UDTs ermöglichen neben der Erweiterbarkeit des SQL Server-Datentypsystems durch Benutzer auch das Definieren komplexer strukturierter Typen.  
  
 UDTs bieten im Hinblick auf die Anwendungsarchitektur zwei wesentliche Vorteile:  
  
-   Starke Kapselung von internem Zustand gegenüber externen Verhaltensweisen (sowohl auf dem Client als auch auf dem Server).  
  
-   Enge Integration mit anderen verwandten Serverfunktionen. Nachdem Sie einen eigenen UDT definiert haben, kann dieser in den gleichen Kontexten verwendet werden wie ein Systemtyp von SQL Server, so u. a. als Spaltendefinitionen, Variablen, Parameter, Funktionsergebnisse, Cursor, Trigger und bei der Replikation.  
  
 Weitere ausführliche Informationen finden Sie in der Onlinedokumentation zu SQL Server für die von Ihnen verwendete Version von SQL Server.  
  
 **SQL Server Books Online (SQL Server-Onlinedokumentation)**  
  
1.  [Benutzerdefinierte CLR-Typen](http://go.microsoft.com/fwlink/?LinkId=98366)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von SQL Server 2005-Objekte In verwaltetem Code](http://msdn.microsoft.com/library/5358a825-e19b-49aa-8214-674ce5fed1da)  
 [ADO.NET Managed Provider und DataSet Developer Center](http://go.microsoft.com/fwlink/?LinkId=217917)
