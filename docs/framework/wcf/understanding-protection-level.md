---
title: "Grundlagen der Schutzebene | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ProtectionLevel-Eigenschaft"
  - "WCF, Sicherheit"
ms.assetid: 0c034608-a1ac-4007-8287-b1382eaa8bf2
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Grundlagen der Schutzebene
Die `ProtectionLevel`\-Eigenschaft ist in vielen anderen Klassen zu finden, z. B. die <xref:System.ServiceModel.ServiceContractAttribute>\-Klasse und die <xref:System.ServiceModel.OperationContractAttribute>\-Klasse.Die Eigenschaft steuert, wie eine Nachricht zum Teil \(oder ganz\) geschützt wird.Dieses Thema erklärt die [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]\-Funktion und wie diese funktioniert.  
  
 Anweisungen zum Festlegen der Schutzebene finden Sie unter [Vorgehensweise: Festlegen der ProtectionLevel\-Eigenschaft](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md).  
  
> [!NOTE]
>  Schutzebenen können nur im Code, nicht in der Konfiguration festgelegt werden.  
  
## Grundlagen  
 Um die Schutzebenenfunktion zu verstehen, sind die folgenden grundlegenden Anweisungen wichtig:  
  
-   Drei grundlegende Ebenen des Schutzes sind für jeden Teil einer Nachricht vorhanden.Die Eigenschaft wird \(bei jedem Auftreten\) auf einen der <xref:System.Net.Security.ProtectionLevel>\-Enumerationswerte festgelegt.In aufsteigender Reihenfolge des Schutzes umfassen sie:  
  
    -   `None`.  
  
    -   `Sign`.Der geschützte Teil wird digital signiert.Dies stellt sicher, dass eine Manipulation am Nachrichtenteil erkannt wird.  
  
    -   `EncryptAndSign`.Der Nachrichtenteil wird verschlüsselt, um Vertraulichkeit sicherzustellen, bevor er signiert wird.  
  
-   Sie können Schutzanforderungen nur für *Anwendungsdaten* mit dieser Funktion festlegen.WS\-Adressierungsheader sind z. B. Infrastrukturdaten und werden deshalb nicht vom `ProtectionLevel` beeinflusst.  
  
-   Wenn der Sicherheitsmodus auf `Transport` festgelegt wird, wird die ganze Nachricht vom Transportmechanismus geschützt.Deshalb hat das Festlegen einer separaten Schutzebene für andere Teile einer Nachricht keine Auswirkungen.  
  
-   Die `ProtectionLevel` stellt eine Möglichkeit für den Entwickler dar, die *Mindestebene* festzulegen, die eine Bindung aufweisen muss.Beim Bereitstellen eines Diensts kann die tatsächliche in der Konfiguration angegebene Bindung die Mindestebene unterstützen oder nicht.Standardmäßig stellt die <xref:System.ServiceModel.BasicHttpBinding>\-Klasse keine Sicherheit bereit \(diese kann allerdings aktiviert werden\).Die Verwendung dieser Klasse in Verbindung mit einem Vertrag, der eine andere Einstellung als `None` hat, löst eine Ausnahme aus.  
  
-   Wenn es der Dienst erfordert, dass die kleinste `ProtectionLevel` für alle Nachrichten `Sign` ist, kann ein Client \(der möglicherweise von einer Nicht\-[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Technologie erstellt wurde\) alle Nachrichten verschlüsseln und signieren \(was über die erforderliche Mindestebene hinausgeht\).In diesem Fall löst [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] keine Ausnahme aus, da der Client über die Mindestebene hinausgeht.Beachten Sie jedoch, dass [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Anwendungen \(Dienste oder Clients\) einen Nachrichtenteil nicht übermäßig schützen, sofern möglich, sondern die Mindestebene einhalten.Außerdem ist zu beachten, dass der Transport den Nachrichtenstrom bei Verwendung von `Transport` als Sicherheitsmodus übermäßig schützt, da in diesem Fall ein Schutz auf niedrigerer Ebene nicht möglich ist.  
  
-   Wenn Sie `ProtectionLevel` ausdrücklich entweder auf `Sign` oder `EncryptAndSign` festlegen, müssen Sie eine Bindung mit aktivierter Sicherheit verwenden. Andernfalls wird eine Ausnahme ausgelöst.  
  
-   Wählen Sie eine Bindung aus, die Sicherheit aktiviert, und legen Sie im Vertrag keine `ProtectionLevel`\-Eigenschaft fest, werden alle Daten verschlüsselt und signiert.  
  
-   Wählen Sie eine Bindung aus, für die keine Sicherheit aktiviert wurde \(für die `BasicHttpBinding`\-Klasse ist die Sicherheit beispielsweise standardmäßig deaktiviert\) und für die `ProtectionLevel` nicht ausdrücklich festgelegt ist, werden keine Anwendungsdaten geschützt.  
  
-   Bei Verwendung einer Bindung, die Sicherheit auf der Transportebene anwendet, werden alle Anwendungsdaten den Transportfunktionen entsprechend geschützt.  
  
-   Wenn Sie eine Bindung verwenden, die die Sicherheit auf der Nachrichtenebene anwendet, werden alle Anwendungsdaten den im Vertrag festgelegten Schutzebenen entsprechend geschützt.Wenn Sie keine Schutzebene festlegen, werden alle Anwendungsdaten in den Nachrichten verschlüsselt und signiert.  
  
-   `ProtectionLevel` kann auf anderen bewertenden Ebenen festgelegt werden.Dem Bewerten ist eine Hierarchie zugeordnet. Diese wird im nächsten Abschnitt erklärt.  
  
## Bewerten  
 Durch Festlegen von `ProtectionLevel` auf der obersten API wird die Ebene für alle untergeordneten Ebenen festgelegt.Wenn `ProtectionLevel` auf einer untergeordneten Ebene auf einen anderen Wert festgelegt ist, werden alle APIs unterhalb dieser Ebene in der Hierarchie auf die neue Ebene geändert \(APIs oberhalb dieser Ebene richten sich nach wie vor nach der obersten Ebene\).Die Hierarchie lautet wie folgt.Attribute auf der gleichen Ebene sind Peers.  
  
 <xref:System.ServiceModel.ServiceContractAttribute>  
  
 <xref:System.ServiceModel.OperationContractAttribute>  
  
 <xref:System.ServiceModel.FaultContractAttribute>  
  
 <xref:System.ServiceModel.MessageContractAttribute>  
  
 <xref:System.ServiceModel.MessageHeaderAttribute>  
  
 <xref:System.ServiceModel.MessageBodyMemberAttribute>  
  
## Programmieren von ProtectionLevel  
 Zum Programmieren von `ProtectionLevel` an einem beliebigen Punkt der Hierarchie legen Sie die Eigenschaft beim Anwenden des Attributs einfach auf einen entsprechenden Wert fest.Weitere Beispiele finden Sie unter [Vorgehensweise: Festlegen der ProtectionLevel\-Eigenschaft](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md).  
  
> [!NOTE]
>  Um die Eigenschaft für Fehler\- und Nachrichtenverträge festlegen zu können, müssen Sie die Funktionsweise dieser Funktionen verstehen.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Vorgehensweise: Festlegen der ProtectionLevel\-Eigenschaft](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md) und [Verwendung von Nachrichtenverträgen](../../../docs/framework/wcf/feature-details/using-message-contracts.md).  
  
## WS\-Adressierungsabhängigkeit  
 In den meisten Fällen ist durch die Verwendung von [ServiceModel Metadata Utility\-Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) zum Generieren eines Clients gewährleistet, dass die Client\- und Dienstverträge identisch sind.Scheinbar identische Verträge können jedoch den Client veranlassen, eine Ausnahme auszulösen.Dies ist der Fall, wenn eine Bindung die WS\-Adressierungsspezifikation nicht unterstützt und mehrere Schutzebenen für den Vertrag festgelegt sind.Beispielsweise unterstützt die <xref:System.ServiceModel.BasicHttpBinding>\-Klasse die Spezifikation nicht oder wenn Sie eine benutzerdefinierte Bindung erstellen, die die WS\-Adressierung nicht unterstützt.Die `ProtectionLevel`\-Funktion ist von der WS\-Adressierungsspezifikation abhängig, um andere Schutzebenen für einen einzelnen Vertrag zu aktivieren.Wenn die Bindung die WS\-Adressierungsspezifikation nicht unterstützt, werden alle Ebenen auf dieselbe Schutzebene festgelegt.Die effektive Schutzebene für alle Bereiche des Vertrags wird auf die höchste Schutzebene festgelegt, die für den Vertrag verwendet wird.  
  
 Dies verursacht möglicherweise ein Problem, das auf den ersten Blick schwer zu debuggen ist.Es ist möglich, einen Dienstvertrag \(eine Schnittstelle\) zu erstellen, der Methoden für mehrere Dienste umfasst,d. h. dieselbe Schnittstelle wird zum Erstellen eines Clients verwendet, der mit vielen Diensten kommuniziert, und die einzelne Schnittstelle umfasst Methoden für alle Dienste.Der Entwickler muss in diesem seltenen Fall darauf achten, nur die Methoden aufzurufen, die für die einzelnen Dienste gelten.Wenn die Bindung die <xref:System.ServiceModel.BasicHttpBinding>\-Klasse ist, können mehrere Schutzebenen nicht unterstützt werden.Ein auf den Client antwortender Dienst kann jedoch auf einen Client mit einer niedrigeren Schutzebene als erforderlich reagieren.In diesem Fall löst der Client eine Ausnahme aus, da er eine höhere Schutzebene erwartet.  
  
 Im folgenden Codebeispiel wird dieses Problem veranschaulicht.Das folgende Beispiel zeigt einen Dienst\- und einen Clientvertrag.Es wird angenommen, dass die Bindung das [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)\-Element ist.Deshalb haben alle Vorgänge im Rahmen eines Vertrags die gleiche Schutzebene.Diese einheitliche Schutzebene wird als maximale Schutzebene für alle Vorgänge bestimmt.  
  
 Der Dienstvertrag lautet:  
  
 [!code-csharp[c_ProtectionLevel#7](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#7)]
 [!code-vb[c_ProtectionLevel#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#7)]  
  
 Im folgenden Codebeispiel wird die Clientvertragsschnittstelle dargestellt.Beachten Sie, dass eine `Tax`\-Methode enthalten ist, die mit einem anderen Dienst verwendet werden sollte:  
  
 [!code-csharp[c_ProtectionLevel#8](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#8)]
 [!code-vb[c_ProtectionLevel#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#8)]  
  
 Wenn der Client die `Price`\-Methode aufruft, wird eine Ausnahme ausgelöst, sobald eine Antwort vom Dienst eingeht.Der Grund hierfür liegt darin, dass der Client keine `ProtectionLevel` im `ServiceContractAttribute` angibt und daher den Standardwert \(<xref:System.Net.Security.ProtectionLevel>\) für alle Methoden, einschließlich der `Price`\-Methode, verwendet.Der Dienst gibt jedoch den Wert unter Verwendung der <xref:System.Net.Security.ProtectionLevel>\-Ebene zurück, da der Dienstvertrag eine einzelne Methode definiert, deren Schutzebene auf <xref:System.Net.Security.ProtectionLevel> festgelegt ist.In diesem Fall löst der Client einen Fehler aus, wenn er die Antwort vom Dienst überprüft.  
  
## Siehe auch  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.MessageContractAttribute>   
 <xref:System.ServiceModel.MessageHeaderAttribute>   
 <xref:System.ServiceModel.MessageBodyMemberAttribute>   
 <xref:System.Net.Security.ProtectionLevel>   
 [Sichern von Diensten](../../../docs/framework/wcf/securing-services.md)   
 [Vorgehensweise: Festlegen der ProtectionLevel\-Eigenschaft](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)   
 [Angeben und Behandeln von Fehlern in Verträgen und Diensten](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)   
 [Verwendung von Nachrichtenverträgen](../../../docs/framework/wcf/feature-details/using-message-contracts.md)