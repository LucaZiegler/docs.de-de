---
title: Was&#39;s neu in ADO.NET
ms.date: 03/30/2017
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
ms.openlocfilehash: eb06681a55f1bd2abffb2e7169fa3bf892cd7313
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="what39s-new-in-adonet"></a>Was&#39;s neu in ADO.NET
Die folgenden Funktionen sind neu in [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] in [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)].  
  
## <a name="sqlclient-data-provider"></a>SqlClient Data Provider  
 Die folgenden Funktionen sind neu in der [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] -Datenanbieter für SQL Server- [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]:  
  
-   Mit den Verbindungszeichenfolgen von ConnectRetryCount und ConnectRetryInterval (<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>) können Sie die resiliente Verbindungsfunktion im Leerlauf steuern.  
  
-   Unterstützung des Streamings von SQL Server zu einer Anwendung unterstützt Szenarien, in denen Daten auf dem Server unstrukturiert ist.  Finden Sie unter [SqlClient-Streamingunterstützung](../../../../docs/framework/data/adonet/sqlclient-streaming-support.md) für Weitere Informationen.  
  
-   Es wurde Unterstützung für asynchrone Programmierung hinzugefügt.  Finden Sie unter [asynchrone Programmierung](../../../../docs/framework/data/adonet/asynchronous-programming.md) für Weitere Informationen.  
  
-   Verbindungsfehler werden jetzt im Protokoll für erweiterte Ereignisse protokolliert. Weitere Informationen finden Sie unter [Datenablaufverfolgung in ADO.NET](../../../../docs/framework/data/adonet/data-tracing.md).  
  
-   SqlClient bietet jetzt Unterstützung für SQL Server hohe Verfügbarkeit, Funktion zur Wiederherstellung im Notfall, AlwaysOn. Weitere Informationen finden Sie unter [SqlClient-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).  
  
-   Ein Kennwort übergeben werden kann, als eine <xref:System.Security.SecureString> bei Verwendung von SQL Server-Authentifizierung. Weitere Informationen finden Sie unter <xref:System.Data.SqlClient.SqlCredential>.  
  
-   Wenn `TrustServerCertificate` lautet "false" und `Encrypt` ist "true", den Servernamen (oder die IP-Adresse) in einem SQL Server-SSL-Zertifikat muss genau übereinstimmen, die Server Name (oder IP-Adresse) in der Verbindungszeichenfolge angegeben. Andernfalls schlägt die Verbindung fehl. Weitere Informationen finden Sie in der Beschreibung der `Encrypt`-Verbindungsoption in <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
     Wenn diese Änderung dazu führt, dass eine vorhandene Anwendung keine Verbindung mehr herstellen kann, können Sie das Problem mithilfe eines der folgenden Verfahren beheben:  
  
    -   Geben Sie ein Zertifikat aus, bei dem im Feld für den allgemeinen Namen (Common Name, CN) oder für den alternativen Antragstellernamen (Subject Alternative Name, SAN) der Kurzname angegeben ist. Diese Lösung funktioniert für die Datenbankspiegelung.  
  
    -   Fügen Sie einen Alias hinzu, der den Kurznamen dem vollqualifizierten Domänennamen zuordnet.  
  
    -   Verwenden Sie den vollqualifizierten Domänennamen in der Verbindungszeichenfolge.  
  
-   SqlClient unterstützt den erweiterten Schutz. Weitere Informationen zu erweitertem Schutz finden Sie unter [Herstellen einer Verbindung mit der Datenbank-Engine mithilfe eines erweiterten Schutzes](http://go.microsoft.com/fwlink/?LinkId=219978).  
  
-   SqlClient unterstützt Verbindungen mit LocalDB-Datenbanken. Weitere Informationen finden Sie unter [SqlClient-Unterstützung für LocalDB](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-localdb.md).  
  
-   `Type System Version=SQL Server 2012;` ist der neue Wert, der an die `Type System Version`-Verbindungseigenschaft übergeben wird. Der `Type System Version=Latest;`-Wert ist jetzt veraltet und wurde `Type System Version=SQL Server 2008;` angeglichen. Weitere Informationen finden Sie unter <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
-   SqlClient bietet zusätzliche Unterstützung für Sparsespalten, eine Funktion, die in SQL Server 2008 hinzugefügt wurde. Wenn die Anwendung bereits auf Daten in einer Tabelle zugreift, die Sparsespalten verwendet, sollten Sie eine Leistungsverbesserung feststellen. Die IsColumnSet-Spalte von <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> gibt an, ob eine Spalte eine Sparsespalte ist und einem Spaltensatz angehört. <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> Gibt an, ob eine Spalte eine Spalte mit geringer Dichte ist (siehe [SQL Server-Schemaauflistungen](../../../../docs/framework/data/adonet/sql-server-schema-collections.md) für Weitere Informationen). Weitere Informationen zu Spalten mit geringer Dichte, finden Sie unter [Spalten mit geringer Dichte verwenden](http://go.microsoft.com/fwlink/?LinkId=224244).  
  
-   Für die Microsoft.SqlServer.Types.dll-Assembly, die die räumlichen Datentypen enthält, wurde ein Upgrade von Version 10.0 auf Version 11.0 vorgenommen. Anwendungen, die auf diese Assembly verweisen, schlagen möglicherweise fehl. Weitere Informationen finden Sie unter [fehlerhafte Änderungen an Funktionen des Datenbankmoduls](http://go.microsoft.com/fwlink/?LinkId=224367).  
  
## <a name="adonet-entity-framework"></a>ADO.NET Entity Framework  
 Durch [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)] werden APIs hinzugefügt, die bei Verwendung von Entity Framework 5.0 neue Szenarien ermöglichen. Weitere Informationen zu Verbesserungen und Features, die zum Entity Framework 5.0 hinzugefügt wurden, finden Sie unter den folgenden Themen: [neues](http://go.microsoft.com/fwlink/?LinkID=251106) und [Entity Framework-Versionen und Versionsverwaltung](http://go.microsoft.com/fwlink/?LinkId=234899).  
  
## <a name="see-also"></a>Siehe auch  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 [Übersicht über ADO.NET](../../../../docs/framework/data/adonet/ado-net-overview.md)  
 [SQL Server und ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)  
 [Neues in WCF Data Services](http://msdn.microsoft.com/library/cf22cad5-b8d9-472b-8d7c-b863b64eaae8)  
 [ADO.NET Managed Provider und DataSet Developer Center](http://go.microsoft.com/fwlink/?LinkId=217917)
