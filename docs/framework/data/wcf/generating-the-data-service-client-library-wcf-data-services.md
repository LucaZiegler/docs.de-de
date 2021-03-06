---
title: Generieren der Datendienst-Clientbibliothek (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- client applications, WCF Data Services
- WCF Data Services, client library
- Add Service Reference dialog box
ms.assetid: 314077c1-ac10-47e1-bed4-940b5462359d
ms.openlocfilehash: 999cbaa98c26d2d00b7e8f319ee87f8b07d7f5c8
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="generating-the-data-service-client-library-wcf-data-services"></a>Generieren der Datendienst-Clientbibliothek (WCF Data Services)
Ein Datendienst, der implementiert die [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] kann ein dienstmetadatendokument an, die das Datenmodell verfügbar gemacht werden, indem Sie beschreibt Zurückgeben der [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] feed. Weitere Informationen finden Sie unter [OData: Dienstmetadatendokument](http://go.microsoft.com/fwlink/?LinkId=186070). Können Sie die **Hinzufügen eines Dienstverweises** Dialogfeld in Visual Studio einen Verweis zum Hinzufügen einer [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]--basierten Diensts. Wenn Sie dieses Tool verwenden, um einen Verweis auf die Metadaten zurückgegebenes Hinzufügen einer [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] feed in ein Clientprojekt, er führt die folgenden Aktionen:  
  
-   Fordert das Dienstmetadatendokument vom Datendienst an und interpretiert die zurückgegebenen Metadaten.  
  
    > [!NOTE]
    >  Die zurückgegebenen Metadaten werden im Clientprojekt als EDMX-Datei gespeichert. Diese EDMX-Datei kann nicht mit dem Entity Data Model-Designer geöffnet werden, da sie nicht das gleiche Format wie eine vom Entity Framework verwendete EDMX-Datei aufweist. Sie können diese Metadatendatei mit dem XML-Editor oder einem beliebigen Texteditor anzeigen. Weitere Informationen finden Sie unter der [ \[MC-EDMX\]: Entity Data Model for Data Services Packaging Format](http://go.microsoft.com/fwlink/?LinkID=178833) Spezifikation  
  
-   Generiert eine Darstellung des Diensts als Entitätscontainerklasse, die vom <xref:System.Data.Services.Client.DataServiceContext> erbt. Diese generierte Entitätscontainerklasse entspricht dem Entitätscontainer, den die Entity Data Model-Tools generieren. Weitere Informationen finden Sie unter [Übersicht über Object Services (Entity Framework)](http://msdn.microsoft.com/library/43014cf9-c9cb-4538-bfbb-197820b60038).  
  
-   Generiert Datenklassen für die in den Dienstmetadaten erkannten Datenmodelltypen.  
  
-   Fügt dem Projekt einen Verweis auf die `System.Data.Services.Client`-Assembly hinzu.  
  
 Weitere Informationen finden Sie unter [wie: Hinzufügen eines Datendienstverweises](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md).  
  
 Die Client-Datendienstklassen können auch generiert werden, mithilfe der [DataSvcUtil.exe](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md) Tool an der Eingabeaufforderung. Weitere Informationen finden Sie unter [Vorgehensweise: Manuelles Generieren von Clientdatendienstklassen](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md).  
  
## <a name="client-data-type-mapping"></a>Zuordnung von Clientdatentypen  
 Bei Verwendung der **Hinzufügen eines Dienstverweises** Dialogfeld in Visual Studio oder die `DataSvcUtil.exe` Tool zum Generieren von clientdatenklassen auf der Grundlage von ein [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] feed, um den primitiven Typen von .NET Framework-Datentypen zugeordnet werden die Daten wie folgt modellieren:  
  
|Datenmodelltyp|.NET Framework-Datentyp|  
|---------------------|------------------------------|  
|`Edm.Binary`|<xref:System.Byte> `[]`|  
|`Edm.Boolean`|<xref:System.Boolean>|  
|`Edm.Byte`|<xref:System.Byte>|  
|`Edm.DateTime`|<xref:System.DateTime>|  
|`Edm.Decimal`|<xref:System.Decimal>|  
|`Edm.Double`|<xref:System.Double>|  
|`Edm.Guid`|<xref:System.Guid>|  
|`Edm.Int16`|<xref:System.Int16>|  
|`Edm.Int32`|<xref:System.Int32>|  
|`Edm.Int64`|<xref:System.Int64>|  
|`Edm.SByte`|<xref:System.SByte>|  
|`Edm.Single`|<xref:System.Single>|  
|`Edm.String`|<xref:System.String>|  
  
 Weitere Informationen finden Sie unter [OData: Primitive Datentypen](http://go.microsoft.com/fwlink/?LinkId=186072).  
  
## <a name="see-also"></a>Siehe auch  
 [WCF Data Services-Clientbibliothek](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)  
 [Schnellstart](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)
