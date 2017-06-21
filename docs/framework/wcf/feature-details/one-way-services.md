---
title: "Unidirektionale Dienste | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dienstverträge [WCF], unidirektionale definieren"
  - "WCF [WCF], unidirektionale Dienstverträge"
  - "Windows Communication Foundation [WCF], unidirektionale Dienstverträge"
ms.assetid: 19053a36-4492-45a3-bfe6-0365ee0205a3
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Unidirektionale Dienste
Das Standardverhalten eines Dienstvorgangs ist das Anforderung\-Antwort\-Muster.Bei einem Anforderung\-Antwort\-Muster wartet der Client auch dann auf die Antwortnachricht, wenn der Dienstvorgang im Code als `void`\-Methode dargestellt wird.Mit einem unidirektionalen Vorgang wird nur eine Nachricht gesendet.Der Empfänger sendet keine Antwortnachricht, und vom Absender wird keine erwartet.  
  
 Verwenden Sie das unidirektionale Entwurfsmuster:  
  
-   Wenn der Client Vorgänge aufrufen muss und vom Ergebnis des Vorgangs auf Vorgangsebene nicht betroffen ist.  
  
-   Wenn die <xref:System.ServiceModel.NetMsmqBinding>\-Klasse oder die <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>\-Klasse verwendet wird.\([!INCLUDE[crabout](../../../../includes/crabout-md.md)] über dieses Szenario finden Sie unter [Warteschlangen in WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md).\)  
  
 Bei einem unidirektionalen Vorgang gibt es keine Antwortnachricht, über die Fehlerinformationen zurück an den Client übertragen werden.Sie können Fehlerbedingungen mit den Funktionen der zugrunde liegenden Bindung, z. B. zuverlässige Sitzungen, ermitteln oder durch den Entwurf eines Duplexdienstvertrags, der zwei unidirektionale Vorgänge verwendet: einen unidirektionalen Vertrag vom Client zum Dienst zum Aufrufen von Dienstvorgängen sowie einen anderen unidirektionalen Vertrag zwischen dem Dienst und dem Client, damit der Dienst über einen vom Client implementierten Rückruf Fehler an den Client zurücksenden kann.  
  
 Wenn Sie einen unidirektionalen Dienstvertrag erstellen möchten, wenden Sie die <xref:System.ServiceModel.OperationContractAttribute>\-Klasse auf alle Vorgänge an, und legen Sie die <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>\-Eigenschaft auf `true` fest, wie im folgenden Beispielcode dargestellt.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOneWayCalculator  
{  
    [OperationContract(IsOneWay=true)]  
    void Add(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Subtract(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Multiply(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Divide(double n1, double n2);  
}  
```  
  
 Den vollständigen Code finden Sie im Beispiel [Unidirektional](../../../../docs/framework/wcf/samples/one-way.md).  
  
## Clients, die mit unidirektionalen Vorgängen blockieren  
 Sie sollten unbedingt berücksichtigen, dass zwar einige unidirektionale Anwendungen gleich nach dem Schreiben der ausgehenden Daten an die Netzwerkverbindung zurückgegeben werden, in anderen Fällen die Implementierung einer Bindung oder eines Diensts jedoch dazu führen kann, dass ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Client mit unidirektionalen Vorgängen blockiert.Im Falle von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Clientanwendungen wird das [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Clientobjekt so lange nicht zurückgegeben, bis die ausgehenden Daten an die Netzwerkverbindung geschrieben wurden.Dies gilt für alle Nachrichtenaustauschmuster, einschließlich unidirektionaler Vorgänge. Dies bedeutet, dass jedes Problem, das beim Schreiben der Daten an den Transport auftritt, verhindert, dass der Client zurückgegeben wird.Je nach dem aufgetretenen Problem könnte das Ergebnis eine Ausnahme sein oder eine Verzögerung beim Senden der Nachrichten an den Dienst.  
  
 Wenn der Transport z. B. den Endpunkt nicht finden kann, wird eine <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=fullName>\-Ausnahme ohne große Verzögerung ausgelöst.Es kann jedoch auch vorkommen, dass der Dienst die Daten aus irgendeinem Grund nicht aus der Verbindung lesen kann. Dadurch wird verhindert, dass der Clienttransport\-Sendevorgang zurückgegeben wird.In diesen Fällen wird beim Überschreiten des <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A?displayProperty=fullName>\-Zeitraums der Clienttransportbindung eine <xref:System.TimeoutException?displayProperty=fullName> ausgelöst, jedoch nicht, bis der Timeoutzeitraum überschritten wurde.Es ist auch möglich, an einen Dienst so viele Nachrichten zu senden, dass diese nach einem bestimmten Punkt nicht vom Dienst verarbeitet werden können.In diesem Fall blockiert der unidirektionale Client so lange, bis der Dienst die Nachrichten verarbeiten kann oder bis eine Ausnahme ausgelöst wird.  
  
 Eine andere Möglichkeit ist die Situation, in der die <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=fullName>\-Diensteigenschaft auf <xref:System.ServiceModel.ConcurrencyMode> festgelegt ist und die Bindung Sitzungen verwendet.In diesem Fall erzwingt der Verteiler die Sortierung der eingehenden Nachrichten \(eine Voraussetzung für Sitzungen\), wodurch verhindert wird, dass die nachfolgenden Nachrichten aus dem Netzwerk gelesen werden, bis der Dienst die vorausgehende Nachricht für diese Sitzung verarbeitet hat.Der Client blockiert wiederum, aber ob eine Ausnahme stattfindet, richtet sich danach, ob die wartenden Daten vor den Timeouteinstellungen auf dem Client verarbeitet werden können.  
  
 Sie können dieses Problem verringern, indem Sie einen Puffer zwischen dem Clientobjekt und dem Sendevorgang des Clienttransports einfügen.Wenn Sie z. B. asynchrone Anrufe oder eine Nachrichtenwarteschlange im Speicher verwenden, wird das Clientobjekt schnell zurückgegeben.Beide Methoden erhöhen eventuell die Funktionalität, aber die Größe des Threadpools und der Nachrichtenwarteschlange erzwingen Beschränkungen.  
  
 Es wird stattdessen empfohlen, die verschiedenen Steuerelemente des Diensts sowie des Clients zu prüfen, um eine optimale Konfiguration auf beiden Seiten zu gewährleisten.Wenn z. B. die Verwendung von Sitzungen die Verarbeitung von Nachrichten in Ihrem Dienst blockiert, können Sie die <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName>\-Eigenschaft auf <xref:System.ServiceModel.InstanceContextMode> festlegen, damit die Nachrichten von einer anderen Dienstinstanz verarbeitet werden können. Außerdem können Sie den <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> auf <xref:System.ServiceModel.ConcurrencyMode> festlegen, um das Senden von Nachrichten von mehr als einem Thread gleichzeitig zu erlauben.Eine andere Methode besteht darin, die Lesekontingente des Diensts und der Clientbindungen zu erhöhen.  
  
## Siehe auch  
 [Unidirektional](../../../../docs/framework/wcf/samples/one-way.md)